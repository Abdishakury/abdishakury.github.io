# Sparkify: Predicting Churn for a Music Streaming Service 

## Table of Contents
* [Introduction](#int)
* [Load and Clean Dataset](#load)
* [Exploratory Data Analysis](#eda)
* [Feature Engineering](#eng)
* [Modelling](#model)
* [Conclusions](#con)

## Introduction
<a class="anchor" id="int"></a>

In this project, I will load and manipulate a music app dataset similar to Spotify with Spark to engineer relevant features for predicting churn. Where Churn is cancelling their service altogether. By identifying these customers before they churn, the business can offer discounts and incentives to stay thereby potentially saving the business revenue. This workspace contains a tiny subset (128MB) of the full dataset available (12GB).

## Installations
 - NumPy
 - Pandas
 - Seaborn
 - Matplotlib
 - PySpark SQL
 - PySpark ML 
 
No additional installations beyond the Anaconda distribution of Python and Jupyter notebooks.

## Load and Clean Dataset
<a class="anchor" id="load"></a>
Our mini-dataset file is `mini_sparkify_event_data.json`. First the dataset must be loaded and cleaned, checking for invalid or missing data - for example, records without userids or sessionids. 

We can now create a Spark Session.

We can now create a Spark Session.
# create a Spark session
spark = SparkSession \
    .builder \
    .appName("Sparkify Project") \
    .getOrCreate()

spark.sparkContext.getConf().getAll()
[('spark.driver.host', 'YOONIS'),
 ('spark.rdd.compress', 'True'),
 ('spark.serializer.objectStreamReset', '100'),
 ('spark.driver.port', '20163'),
 ('spark.master', 'local[*]'),
 ('spark.submit.pyFiles', ''),
 ('spark.executor.id', 'driver'),
 ('spark.app.id', 'local-1650402062669'),
 ('spark.submit.deployMode', 'client'),
 ('spark.ui.showConsoleProgress', 'true'),
 ('spark.app.name', 'Sparkify Project')]

# load in the dataset
df = spark.read.json("mini_sparkify_event_data.json")

# print the schema
df.printSchema()

root
 |-- artist: string (nullable = true)
 |-- auth: string (nullable = true)
 |-- firstName: string (nullable = true)
 |-- gender: string (nullable = true)
 |-- itemInSession: long (nullable = true)
 |-- lastName: string (nullable = true)
 |-- length: double (nullable = true)
 |-- level: string (nullable = true)
 |-- location: string (nullable = true)
 |-- method: string (nullable = true)
 |-- page: string (nullable = true)
 |-- registration: long (nullable = true)
 |-- sessionId: long (nullable = true)
 |-- song: string (nullable = true)
 |-- status: long (nullable = true)
 |-- ts: long (nullable = true)
 |-- userAgent: string (nullable = true)
 |-- userId: string (nullable = true)

## Exploratory Data Analysis
<a class="anchor" id="eda"></a>

### Define Churn

A column `Churn` will be created to use as the label for our model. `Cancellation Confirmation` events is used to define churn, which happen for both paid and free users. We will assign a 1 where a user has churned and a 0 where they have not churned.

### Explore Data
Exploratory data analysis will  be performed to observe the behavior for users who stayed vs users who churned. Starting by exploring aggregates on these two groups of users, observing how much of a specific action they experienced per a certain time unit or number of songs played.


### EDA for Users that Stayed vs Users that Churned
Now we can examine behaviour of those who churned vs those who did not churn. First we will visualise those who churned vs those who stayed.

# convert to pandas for visualisation
df_churn = df_churn.toPandas()

# plot the number of users that churned
plt.figure(figsize = [8,6])
ax = sns.barplot(data = df_churn, x = 'churn', y='count')
plt.title("Numbers of Users That Churned");


Now we can do the same process for customers who didn't churn.

sawiro

We can see from the above plots that length distribution is very similar for users that churned and those who stayed. This won't be very useful for predicting customer churn. Let's try a categorical feature: gender.

# I want to convert to pandas for visualisation

sawiro

From the above chart, we can see that the most popular action for both users that stayed and those that churned was to skip to the next song. We can also see that churned users rolled the ad and thumbs down songs more. Those who were more likely to stay performed more thumbs up actions, added friends and also added songs to playlist.

### Calculating Songs per Hour
We can now turn our attention to calculating the number of songs listened to by churn and non churn users per hour. 

sawir

From above we can see that there is a peak of songs played between 3pm and 8pm. Next we will examine users who churned by using the same process.

### Songs Per Session for Users who Churned vs. Those who Stayed
We can plot this in a simple way which will allow us to compare those who churned and those who stayed in a bar chart by getting the averages for both groups.

sawiro


Most users were based in CA. More users in MI, KY, and OH states churned than stayed. This may be difficult to engineer a useful feature for when it comes to modelling. Let's leave this for now and move onto another column from our dataset; operating systems and browsers.

### UserAgent: Operating System and Browsers
Now we can extract the Operating System a user is on to understand if this has an effect on churn.

sawiro

Chrome was the most popular browser. Firefox users were most likely to churn. Internet Explorer had the fewest number of users that churned. There is no clear issue with browsers which is making users churn. Therefore this won't be used in our model.

### Days Since Registration for Sparkify
Finally, we can look at the number of days since a user had registered.

sawiro

Now I need to minus these and work that out in days by minus the registration from ts

# I use to Pandas for the plot boxplot

sawir

# Feature Engineering
<a class="anchor" id="eng"></a>

Now that EDA has been performed, we can build out the features that seem most promising to train our model on.

The features we will build out are:
- Categorical:
 - gender
 - level

- Numerical:
 - number of songs per session
 - number of rollads actions
 - number of thumb down actions
 - number of thumbs up actions
 - number of friends added
 - number of songs added to playlist
 - number of different artists listened to on Sparkify
 - number of days since registering
 
We will also then add a churn label and join these all together. This will create a dataFrame where each row represents information pertaining to each individual user. Once we drop the userId, this dataframe can be vectorised, standarised and fed into our different machine learning algorithms.

First we will take our categorical variables and convert these into numeric variables, ready for our model.


### Gender

Our first feature is gender which is a categorical one. We will assign a 1 for 'female' and a 0 for 'male'.

sawir



### Average Number of songs per session
Our third feature is average number of songs per session for each user.

sawiro


### Number of rollads actions
Next feature we can consider is number of roll advert actions. This had a higher number of roll ad count for those who churned since those who use the app for free are shown ads whereas paid subscribers aren't shown ads.

sawiro


### Number of thumb down actions
The fifth feature we can add to our feature dataframe is thumbs down. Users who had churned in the past had performed more thumbs down actions than those who stayed with the service. 

sawir

### Number of thumbs up actions
We can do the same for thumb up actions. Users who stayed with the service had performed more thumbs up actions in the past.

sawir

### Number of friends added
Similarly, number of friends added can indicate if a user is likely to churn or not. In the past, those who added more friends stayed with the app.

sawir

### Number of songs added to playlist
Again, those who added more songs to their playlists had stayed with the service so this can provide an indication of whether a user is likely to churn.

sawiro

### Number of different Artists Listened to on Sparkify
As we discovered in EDA, users that listened to more diverse artists were less likely to churn.

sawir

### Number of Days Since Registering
Number of days since registering also looked useful from our EDA. We saw that users who had a shorter number of days since registering churned more than those who had used the service for a longer time.

sawir:df_feature

Now we have a dataframe with all the features we can into our model where each row represents a user.However first we need to do some preprocessing.

sawir:df_feature2

sawir:df_feature3

sawir:df_feature4

### Standardisation
Now that we have our vectors we can standardise our values. This is important for our machine learning model so that those features with the highest values don't dominate the results and so that we can make the individual features look like standard normally distributed data.

sawir:df_feature5

## Train / Test / Validation Split
Let's check how many records we have in total is 225 as it should be.

sawir:df_feature6

This count is what we would expect, now we can split our data into train, test and validation sets. Here we will do a 60:20:20 split and include a seed so we can reproduce the result. I've included the same seed for the different machine learning models so that my results can be reproduced.

sawir:df_feature7

# Modelling
<a class="anchor" id="model"></a>

Now we have created our features dataFrame with only numeric variables, we can split the full dataset into train, test, and validation sets. We will test out different machine learning classification algorithms including:
 - Logistic Regression
 - Random Forest Classifier
 - Gradient-Boosted Tree Classifier
 - Linear Support Vector Machine
 - Naive Bayes
 
We will use these classification algorithms since churn prediction is a binary classification problem, meaning that customers will either churn (1) or they will stay (0) in a certain period of time. 

### Metrics
We will evaluate the accuracy of the various models, tuning parameters as necessary. We will finally determine our winning model based on test accuracy and report results on the validation set. Since the churned users are a fairly small subset, I will use F1 score as the metric to optimize. F1 is a measure of the model's accuracy on a dataset and is used to evaluate binary classification systems like we have here. F1-score is a way of combining the precision and recall of the model and gives a better measure of the incorrectly classified cases than accuracy metric. F1 is also better for dealing with imbalanced classes like we have here.

Now we can start modelling. When we identify the model with the best F1 score, accuracy and time we will then tune the model.

The models I have selected are below with the reasons why these have been chosen. Each model that has been chosen is suitable for our binary classification problem of predicting churn.

- **Logistic Regression:** Logistic regression is the first machine learning algorithm we can try. Logistic regression is a reliable machine learning algorithm to try since this is a binary classification problem and logistic regression provides a model with good explainability. Logistic regression is also easy to implement, interpret and is efficient to train. It is also less inclined to overfitting.       
- **Random Forest:** Random Forest is a powerful supervised learning algorithm that can be used for classification. RF is an ensemble method that creates multiple decision trees to make predictions and takes a majority vote of decisions reached. This can help avoid overfitting. RF is also robust and has good performance on imbalanced datasets like we have here.        
- **Gradient Boosted Tree Classifier:** GBT provides good predictive accuracy. This works by building one tree at a time where each new tree helps correct errors made by the previous tree compared to RF which builds trees independently. There is a risk of overfitting with GBT so this needs to be considered. However GBT performs well with unbalanced data which we have here.    
- **Linear SVC:** SVC is another supervised learning binary classification algorithm. It works well with clear margins of separations between classes and is memory efficient.    
- **Naive Bayes:** Finally, we will try Naive Bayes. This is another classifier algorithm that is easy to implement and is fast.

### Training the Models & Evaluating the Model Performance
Steps:
 - Instantiate 
 - Fit Models on Train
 - Predicting
 - Evaluating


sawir:df_feature8

sawir:df_feature9

sawir:df_feature10

Now that we have our results we can choose our best model. Random Forest and Gradient Boosted Trees performed well but random forest was faster so I will choose this one to tune.

## Model Tuning for Best Models:
Now we can tune our model using paramGridbuilder and CrossValidator. I am going to select Random Forest since this is the best compromise for F1 score, accuracy, and time to run. Random Forrest had a F1 score of 0.87 and accuracy of 0.88 and took 2 min 57s compared to GTB which achieved a similar score of 0.88 for both F1 score and accuracy but took 3 min 51s. 

### Random Forest
sawir:df_feature11

## Parameters

I will select numTrees and maxDepth for our RF model tuning. 
- **NumTrees**: I have chosen to go up to 100 trees to improve performance. Since these trees are individual randomised models in an ensemble there is not a great risk of overfitting with this numTrees parameter.
- **Maxdepth**: I have chosen a max of 15 to reduce the possibility of overfitting. Anything over 15 would increase the risk of overfitting greatly.
- **Numfolds**: I originally had numFolds = 5 but had to change to 3 to speed up the process.

sawir:df_feature12

### Best Model Performance Results:
We can now get the final results for our random forest model.

sawir:df_feature13

sawir:df_feature14

#### Feature Importance:
Finally, we can check the feature importance for our best model and plot this in a chart.

sawir:df_feature15

sawir:df_feature16

# Conclusions
<a class="anchor" id="con"></a>

We started the project with a small dataset of just 128MB and 225 unique customers. After loading and cleaning our data we explored the dataset for useful features to predict churn and were able to build out the most promising features. We then preprocessed these and used the features with different machine learning algorithms. Random Forest performed the best, so we tuned the model and achieved an accuracy and F1 score of 0.88.

### Business Impact:

Now, Sparkify can use this information to target customers who are likely to churn and offer attractive incentives to stay, thereby saving Sparkify revenue and getting the customer a nice deal. Since we found that newer customers are more likely to churn, we could target them with a nice free trial of the premium service without those pesky ads! Sparkify could also work on music recommendation system so they can recommend songs that users will enjoy more and thumbs down less.

### Project Reflection

From this project I have learned how to manipulate datasets with Spark to engineer relevant features for predicting churn. I used Spark MLib to build machine learning models to predict churn. It was interesting to start with a dataset which had the customers' user interactions and then use this to predict whether or not they were likely to churn. The best model was the Random Forest classifier which achieved an accuracy and F1 score of 0.88. It was interesting to build my first model for predicting churn in pyspark as opposed to pandas. 

### Future Work

This project could have been improved by:
 - doing more feature engineering to select the best features to get a better score
 - considered overfitting problems in more depth
 - analysing mispredicted users

## References

https://stackoverflow.com/questions/21702342/creating-a-new-column-based-on-if-elif-else-condition     
https://stackoverflow.com/questions/46921465/extract-substring-from-text-in-a-pandas-dataframe-as-new-column     
https://developers.whatismybrowser.com/useragents/explore/layout_engine_name/trident/     
https://sparkbyexamples.com/pyspark/pyspark-when-otherwise/     
https://stackoverflow.com/questions/52943627/convert-a-pandas-dataframe-to-a-pyspark-dataframe     
https://stackoverflow.com/questions/29600673/how-to-delete-columns-in-pyspark-dataframe      
https://stackoverflow.com/questions/48738354/having-troubles-joining-3-dataframes-pyspark     
https://stackoverflow.com/questions/59886143/spark-dataframe-how-to-keep-only-latest-record-for-each-group-based-on-id-and    
https://stackoverflow.com/questions/46956026/how-to-convert-column-with-string-type-to-int-form-in-pyspark-data-frame    
https://medium.com/swlh/logistic-regression-with-pyspark-60295d41221     
https://towardsdatascience.com/machine-learning-with-pyspark-and-mllib-solving-a-binary-classification-problem-96396065d2aa     
https://spark.apache.org/docs/latest/ml-classification-regression.html#logistic-regression     
https://stackoverflow.com/questions/60772315/how-to-evaluate-a-classifier-with-apache-spark-2-4-5-and-pyspark-python    
https://stackoverflow.com/questions/60772315/how-to-evaluate-a-classifier-with-apache-spark-2-4-5-and-pyspark-python    
https://spark.apache.org/docs/2.2.0/ml-classification-regression.html    
https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html      
https://stackoverflow.com/questions/32565829/simple-way-to-measure-cell-execution-time-in-ipython-notebook     
https://www.silect.is/blog/random-forest-models-in-spark-ml/     
https://stackoverflow.com/questions/75440/how-do-i-get-the-string-with-name-of-a-class

































## Project Motivation
For this project I was interested in predicting customer churn for a fictional music streaming company: Sparkify. 

The project involved:
 - Loading and cleaning a small subset (128MB) of a full dataset available (12GB) 
 - Conducting Exploratory Data Analysis to understand the data and what features are useful for predicting churn
 - Feature Engineering to create features that will be used in the modelling process
 - Modelling using machine learning algorithms such as Logistic Regression, Random Forest, Gradient Boosted Trees, Linear SVM, Naive Bayes 

## File Descriptions
There is one exploratory notebook and html file of the notebook available here to showcase my work in predicting churn. Markdown cells were used throughout to explain the process taken.

## Medium Blog Post 
The main findings of the code can be found at the Medium Blog post available [here]() explaining the technical details of my project.
A Random Forest Classifier was chosen to be the best model by evaluating F1 score and accuracy metrics. The final model achieved an F1 and Accuracy score of 0.88. 

## Licensing, Authors, Acknowledgements, etc.
I'd like to acknowledge Udacity for the project idea and workspace.
