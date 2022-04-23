# Sparkify: Predicting Churn for a Music Streaming Service 

## Table of Contents
* [Introduction](#int)
* [Project Motivation](#mot)
* [File Descriptions](#des)
* [Load and Clean Dataset](#load)
* [Exploratory Data Analysis](#eda)
* [Feature Engineering](#eng)
* [Modelling](#model)
* [Business Impact](#bus)
* [Project Reflection](#refl)
* [Future Work](#fut)
* [Conclusions](#con)
* [Github Page Blog Post](#github)
* [Licensing, Authors, Acknowledgements](#lic)
* [References](#refe)
* 

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

## Project Motivation
<a class="anchor" id="mot"></a>
For this project I was interested in predicting customer churn for a fictional music streaming company: Sparkify. 

The project involved:
 - Loading and cleaning a small subset (128MB) of a full dataset available (12GB) 
 - Conducting Exploratory Data Analysis to understand the data and what features are useful for predicting churn
 - Feature Engineering to create features that will be used in the modelling process
 - Modelling using machine learning algorithms such as Logistic Regression, Random Forest, Gradient Boosted Trees, Linear SVM, Naive Bayes 

## File Descriptions
<a class="anchor" id="des"></a>
There is one exploratory notebook and html file of the notebook available here to showcase my work in predicting churn. Markdown cells were used throughout to explain the process taken.

## Load and Clean Dataset
<a class="anchor" id="load"></a>
Our mini-dataset file is `mini_sparkify_event_data.json`. First the dataset must be loaded and cleaned, checking for invalid or missing data - for example, records without userids or sessionids. 

We can now create a Spark Session.

### create a Spark session
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

### load in the dataset
df = spark.read.json("mini_sparkify_event_data.json")

### print the schema
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

### convert to pandas for visualisation
df_churn = df_churn.toPandas()

### plot the number of users that churned
plt.figure(figsize = [8,6])
ax = sns.barplot(data = df_churn, x = 'churn', y='count')
plt.title("Numbers of Users That Churned");


Now we can do the same process for customers who didn't churn.

![churn_users](https://user-images.githubusercontent.com/83236722/164799111-98c66c97-41e5-4363-b30d-6ada69c030bd.png)

![hist_curn](https://user-images.githubusercontent.com/83236722/164799415-a811e151-6a68-4db8-a9ee-bc3ba8a9576b.png)


We can see from the above plots that length distribution is very similar for users that churned and those who stayed. This won't be very useful for predicting customer churn. Let's try a categorical feature: gender.

### I want to convert to pandas for visualisation

![hist_curn2](https://user-images.githubusercontent.com/83236722/164799522-ff7de338-d763-4b96-8575-8f06dd002f78.png)

![df_gender](https://user-images.githubusercontent.com/83236722/164799635-51595753-82b5-4117-92eb-441901e170d5.png)

![df_gender_curn](https://user-images.githubusercontent.com/83236722/164799904-cc29088d-00bb-4251-8446-7171b2001f16.png)


![level_show](https://user-images.githubusercontent.com/83236722/164800671-ed79e749-ad29-4d16-ba99-23ae09350877.png)

![df_gender_curn2](https://user-images.githubusercontent.com/83236722/164800815-4ccc0b94-dcd5-4b1c-ac63-f49aa6843ce1.png)


From the above chart, we can see that the most popular action for both users that stayed and those that churned was to skip to the next song. We can also see that churned users rolled the ad and thumbs down songs more. Those who were more likely to stay performed more thumbs up actions, added friends and also added songs to playlist.

![df_page](https://user-images.githubusercontent.com/83236722/164801028-54b5b8ef-811b-46be-b754-3c99ba1cca1d.png)

![df_page2](https://user-images.githubusercontent.com/83236722/164801039-9385ed9f-9b76-4c15-b4a4-c9031fcbd271.png)


![df_page3](https://user-images.githubusercontent.com/83236722/164800945-0a47ad6c-b1f7-41ed-9add-db014bb77552.png)


### Calculating Songs per Hour
We can now turn our attention to calculating the number of songs listened to by churn and non churn users per hour. 

![songs_in_hour](https://user-images.githubusercontent.com/83236722/164801157-31c9588f-bc1b-4987-aeb6-41db8faa9315.png)

![songs_in_hour2](https://user-images.githubusercontent.com/83236722/164801209-525d84b5-a14e-4915-839e-02e23a5c2239.png)


From above we can see that there is a peak of songs played between 3pm and 8pm. Next we will examine users who churned by using the same process.

### Songs Per Session for Users who Churned vs. Those who Stayed
We can plot this in a simple way which will allow us to compare those who churned and those who stayed in a bar chart by getting the averages for both groups.


![average_songs_table](https://user-images.githubusercontent.com/83236722/164801327-86137a3b-c0ae-4fed-8f55-c35223da687b.png)


![average_songs_table2](https://user-images.githubusercontent.com/83236722/164801361-b2c96b64-a01b-41b9-9a40-392e0ea4e7de.png)


### UserAgent: Operating System and Browsers
Now we can extract the Operating System a user is on to understand if this has an effect on churn.

![location_count](https://user-images.githubusercontent.com/83236722/164803574-18f7aad2-f59e-4ede-a769-f503ddf59b93.png)


![location_count2](https://user-images.githubusercontent.com/83236722/164803604-1005194c-5672-40cf-bc19-70b2c487ac63.png)

Most users were based in CA. More users in MI, KY, and OH states churned than stayed. This may be difficult to engineer a useful feature for when it comes to modelling. Let's leave this for now and move onto another column from our dataset; operating systems and browsers.

![web_browsers](https://user-images.githubusercontent.com/83236722/164810511-7db1a521-923b-4bc9-8411-7ed03c3c7a67.png)

![web_browsers_by_devices](https://user-images.githubusercontent.com/83236722/164810950-40a3590a-6dc7-46a2-ace3-bcac6e031e3b.png)


![web_browsers_by_devices2](https://user-images.githubusercontent.com/83236722/164811051-d6956aa3-99b3-4f57-b4a6-345e749e6ef6.png)

Windows was the most used. Linux users have the highest rate of churn. It is very few customers that this has affected therefore this won't be used in our model.

![browser_count](https://user-images.githubusercontent.com/83236722/164814327-0fc8400a-5682-4de1-a897-1af8f8737cd8.png)

![web_browsers2](https://user-images.githubusercontent.com/83236722/164811437-857e6185-fbf1-4e02-91d4-54daaba2344c.png)

Chrome was the most popular browser. Firefox users were most likely to churn. Internet Explorer had the fewest number of users that churned. There is no clear issue with browsers which is making users churn. Therefore this won't be used in our model.


### Days Since Registration for Sparkify
Finally, we can look at the number of days since a user had registered.

![df_days](https://user-images.githubusercontent.com/83236722/164814825-1cefa7e4-8a8f-4845-b7c8-411aad49d9f5.png)


![df_days2](https://user-images.githubusercontent.com/83236722/164814838-4ca1fbc9-c084-4cd4-a602-dc48d716b499.png)


Now I need to minus these and work that out in days by minus the registration from ts

![df_days3](https://user-images.githubusercontent.com/83236722/164814962-8a4a8c22-8ddf-4869-8306-766e73952c22.png)


### I use to Pandas for the plot boxplot

![boxplot](https://user-images.githubusercontent.com/83236722/164815018-c2ddeee5-2a58-494d-acc2-e98800b4f916.png)

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

![gender_userId](https://user-images.githubusercontent.com/83236722/164816146-f5e1c3a3-7a5a-40ee-affe-fc5e78e17296.png)

![gender_userId2](https://user-images.githubusercontent.com/83236722/164816180-525b96c5-5b86-4d75-bf1d-4cde6f9a644d.png)

![userId_level](https://user-images.githubusercontent.com/83236722/164816248-be7c2288-857f-4082-bc43-8c592413d1d1.png)


### Average Number of songs per session
Our third feature is average number of songs per session for each user.

![userId_level2](https://user-images.githubusercontent.com/83236722/164816273-379bab7f-a16c-4485-a360-830c92ee5285.png)


![userId_level3](https://user-images.githubusercontent.com/83236722/164816306-82295a69-9281-427d-8f5b-bd03ff38e374.png)


### Number of rollads actions
Next feature we can consider is number of roll advert actions. This had a higher number of roll ad count for those who churned since those who use the app for free are shown ads whereas paid subscribers aren't shown ads.

![userId_level4](https://user-images.githubusercontent.com/83236722/164816328-9ae119a3-69f2-432b-9c74-f39d68c7b5b4.png)

### Number of thumb down actions
The fifth feature we can add to our feature dataframe is thumbs down. Users who had churned in the past had performed more thumbs down actions than those who stayed with the service. 

![userId_level5](https://user-images.githubusercontent.com/83236722/164816366-ac1e8b5a-5d59-4881-a925-a8cdb30f70bd.png)

### Number of thumbs up actions
We can do the same for thumb up actions. Users who stayed with the service had performed more thumbs up actions in the past.

![userId_level6](https://user-images.githubusercontent.com/83236722/164816407-b95b1015-9100-4108-a5d1-cf77bb7d8fe0.png)

### Number of friends added
Similarly, number of friends added can indicate if a user is likely to churn or not. In the past, those who added more friends stayed with the app.

![userId_level7](https://user-images.githubusercontent.com/83236722/164816444-e229ad6e-53ac-4071-8364-a44856e95a7e.png)

### Number of songs added to playlist
Again, those who added more songs to their playlists had stayed with the service so this can provide an indication of whether a user is likely to churn.

![userId_level8](https://user-images.githubusercontent.com/83236722/164816481-fa135e8b-207d-4b8b-99a7-c1775b5a131a.png)

### Number of different Artists Listened to on Sparkify
As we discovered in EDA, users that listened to more diverse artists were less likely to churn.

![userId_level9](https://user-images.githubusercontent.com/83236722/164816512-00ae573f-4473-4910-b558-a7ddb02fc73a.png)


### Number of Days Since Registering
Number of days since registering also looked useful from our EDA. We saw that users who had a shorter number of days since registering churned more than those who had used the service for a longer time.

![df_feature](https://user-images.githubusercontent.com/83236722/164816540-9522832b-2991-444c-aa74-178ea53831bc.png)

Now we have a dataframe with all the features we can into our model where each row represents a user.However first we need to do some preprocessing.

![df_feature2](https://user-images.githubusercontent.com/83236722/164816548-1f071af2-699b-42e1-b2db-c7a336f52272.png)

![df_feature3](https://user-images.githubusercontent.com/83236722/164816555-7f39e2cd-2ad0-4625-a694-0dc9cf926105.png)


![df_feature4](https://user-images.githubusercontent.com/83236722/164816562-ea1ce5ba-e512-46ee-b2cd-93ee5abd69af.png)

### Standardisation
Now that we have our vectors we can standardise our values. This is important for our machine learning model so that those features with the highest values don't dominate the results and so that we can make the individual features look like standard normally distributed data.

![df_feature5](https://user-images.githubusercontent.com/83236722/164816575-d4a4416a-49f0-4011-96b0-8dddad7a3188.png)


### Train / Test / Validation Split
Let's check how many records we have in total is 225 as it should be.

![df_feature6](https://user-images.githubusercontent.com/83236722/164816590-1dfc0035-7571-404b-85cd-95de628e6ed4.png)


This count is what we would expect, now we can split our data into train, test and validation sets. Here we will do a 60:20:20 split and include a seed so we can reproduce the result. I've included the same seed for the different machine learning models so that my results can be reproduced.

![df_feature7](https://user-images.githubusercontent.com/83236722/164816598-2ad40d3c-7ca6-44c6-ad2f-b51afff46775.png)

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

![df_feature8](https://user-images.githubusercontent.com/83236722/164816684-b8209c7f-679a-48ab-9bbd-35dfa8b802d5.png)

![df_feature9](https://user-images.githubusercontent.com/83236722/164816721-eb8794c5-f959-47a7-b5d6-96128b207d11.png)

![df_feature10](https://user-images.githubusercontent.com/83236722/164816730-4c168a5d-3f79-49b8-bf0e-58023010f3d2.png)

Now that we have our results we can choose our best model. Random Forest and Gradient Boosted Trees performed well but random forest was faster so I will choose this one to tune.

## Model Tuning for Best Models:
Now we can tune our model using paramGridbuilder and CrossValidator. I am going to select Random Forest since this is the best compromise for F1 score, accuracy, and time to run. Random Forrest had a F1 score of 0.87 and accuracy of 0.88 and took 2 min 57s compared to GTB which achieved a similar score of 0.88 for both F1 score and accuracy but took 3 min 51s. 

### Random Forest

![df_feature11](https://user-images.githubusercontent.com/83236722/164816751-6f1f89ac-6c64-4301-8d51-d76453c4a14c.png)

## Parameters

I will select numTrees and maxDepth for our RF model tuning. 
- **NumTrees**: I have chosen to go up to 100 trees to improve performance. Since these trees are individual randomised models in an ensemble there is not a great risk of overfitting with this numTrees parameter.
- **Maxdepth**: I have chosen a max of 15 to reduce the possibility of overfitting. Anything over 15 would increase the risk of overfitting greatly.
- **Numfolds**: I originally had numFolds = 5 but had to change to 3 to speed up the process.

![df_feature12](https://user-images.githubusercontent.com/83236722/164816763-89ce7069-eb85-4ba2-8668-72028abe7f6e.png)

### Best Model Performance Results:
We can now get the final results for our random forest model.

![df_feature13](https://user-images.githubusercontent.com/83236722/164816767-ab7f57d6-2e1f-4d0c-ace0-0dcb05baa976.png)

![df_feature14](https://user-images.githubusercontent.com/83236722/164816783-44b424ff-c05b-43de-91c5-60e473a36722.png)

### Feature Importance:
Finally, we can check the feature importance for our best model and plot this in a chart.

![df_feature15](https://user-images.githubusercontent.com/83236722/164816792-8d05dddf-2db6-4823-a0f4-82f748225751.png)


![df_feature16](https://user-images.githubusercontent.com/83236722/164816804-d19997f0-69ba-41f4-91ff-210a3566a242.png)


# Business Impact
<a class="anchor" id="bus"></a>

Now, Sparkify can use this information to target customers who are likely to churn and offer attractive incentives to stay, thereby saving Sparkify revenue and getting the customer a nice deal. Since we found that newer customers are more likely to churn, we could target them with a nice free trial of the premium service without those pesky ads! Sparkify could also work on music recommendation system so they can recommend songs that users will enjoy more and thumbs down less.

# Project Reflection
<a class="anchor" id="refl"></a>

From this project I have learned how to manipulate datasets with Spark to engineer relevant features for predicting churn. I used Spark MLib to build machine learning models to predict churn. It was interesting to start with a dataset which had the customers' user interactions and then use this to predict whether or not they were likely to churn. The best model was the Random Forest classifier which achieved an accuracy and F1 score of 0.88. It was interesting to build my first model for predicting churn in pyspark as opposed to pandas. 

# Future Work
<a class="anchor" id="fut"></a>

This project could have been improved by:
 - doing more feature engineering to select the best features to get a better score
 - considered overfitting problems in more depth
 - analysing mispredicted users

# Conclusions
<a class="anchor" id="con"></a>

We started the project with a small dataset of just 128MB and 225 unique customers. After loading and cleaning our data we explored the dataset for useful features to predict churn and were able to build out the most promising features. We then preprocessed these and used the features with different machine learning algorithms. Random Forest performed the best, so we tuned the model and achieved an accuracy and F1 score of 0.88.

## Github Page Blog Post 
<a class="anchor" id="github"></a>
The main findings of the code can be found at the Medium Blog post available [here]() explaining the technical details of my project.
A Random Forest Classifier was chosen to be the best model by evaluating F1 score and accuracy metrics. The final model achieved an F1 and Accuracy score of 0.88. 

## Licensing, Authors, Acknowledgements, etc.
<a class="anchor" id="lic"></a>
I'd like to acknowledge Udacity for the project idea and workspace.

# References
<a class="anchor" id="refe"></a>

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
