# A closer look into the data of Seattle’s Airbnb market


### Table of Contents

1. [The Libraries That I Have Used](#libraries)
2. [My Project Motivation](#motivation)
3. [File Descriptions](#files)
4. [Summary Of The Results](#results)
5. [Acknowledgements](#acknowledgements)

## The Libraries That I Have Used <a name="libraries"></a>

The Anaconda Python 3.0 distribution was used to accomplish the project. In addition, the following python libraries have been implemented: 

1. Collections
2. Matplotlib 
3. NLTK
4. NumPy
5. Pandas
6. Seaborn
7. Sklearn

## My Project Motivation<a name="motivation"></a>

I was curious to look into the AirBnB dataset for Seattle. I needed to discover more about pricing patterns, customer feedback, and pricing forecasting. Some of the questions I've looked into are: 

# Question 1 - PRICE ANALYSIS

1. What is the peak season in Seattle and how does pricing change with the seasons?
2. How does pricing differ by neighbourhood, and which Seattle neighbourhoods are the most expensive?
3. What effect does the kind of property in an area have on the price of the most costly neighbourhoods and the most prevalent property types?

![image](https://user-images.githubusercontent.com/83236722/142714387-a5d24721-3cd0-43a1-b91c-1ee084032af7.png)

#### FINDINGS

According to the chart above, the peak months are June through August, with July being the highest.
With summer in full swing and low potential of rain, the chart validates my hypothesis that these months in Seattle have the optimum weather. 

Furthermore, it looks likely that the year begins gradually, with the minimum average price in January.
Prices begin to rise again around April/May respectively, as we approach Spring and the holiday season.and November/December for Winter holiday. 

![image](https://user-images.githubusercontent.com/83236722/142714474-a615c826-751c-4efe-afa0-27b7132103be.png)

![image](https://user-images.githubusercontent.com/83236722/142714500-10e6f40c-8e4a-47f4-86e8-6c81cc099e6d.png)

![image](https://user-images.githubusercontent.com/83236722/142714518-d86426c5-d275-4d3b-894d-4daaaacb132e.png)

#### FINDINGS

According to the above analysis, pricing variations between neighbourhoods are unavoidable.
With an average price of $231, the Southeast Magnolia area appears to be the most expensive of all. 

Followed by Portage Bay at $227.

Rainier Beach appears to be the cheapest, with an average price of $68.

![image](https://user-images.githubusercontent.com/83236722/142714553-0aaed328-0350-4185-842b-77c21eec42dc.png)

![image](https://user-images.githubusercontent.com/83236722/142714653-9d75a896-1b63-4686-8db1-957dbcaa6606.png)

#### FINDINGS

We concentrated on the top 5 most expensive neighbourhoods from the above analysis, along with Houses and Apartments, because we recognize they make up a significant portion of property types based on the previous analysis. 

Houses in Portage Bay are the most expensive, followed by Houses in West Queen Anne and Westlake, as seen above.
It's worth noting that in Westlake, both houses and apartments are almost the same price.  

# Question 2 - SENTIMENT ANALYSIS OF REVIEWS

4. How can we classify reviews focused on sentiments?
5. Can we correlate positive and negative attitudes from reviews to neighbourhoods to see which neighbourhoods have higher positive sentiments and which have higher negative sentiments?
6. Is it possible to look into some of the worst reviews for additional insights?

![image](https://user-images.githubusercontent.com/83236722/142714716-bf59726b-866e-40c9-9175-222ecc984d8c.png)

![image](https://user-images.githubusercontent.com/83236722/142714729-da857085-9d9f-45fa-9bdb-f42e8e04f34a.png)

![image](https://user-images.githubusercontent.com/83236722/142714749-08f93800-5957-4bb6-a037-6a64dc857580.png)

#### Visualize top neighbourhoods based on reviews
![image](https://user-images.githubusercontent.com/83236722/142714761-590d945d-4cfb-439d-9e87-28f1a22bd934.png)

#### Visualize bottom 10 neighbourhoods based on reviews
![image](https://user-images.githubusercontent.com/83236722/142714811-79544957-178c-41d1-9704-774f89543d25.png)

#### FINDINGS

Some of the best-rated neighbourhoods include Roxhill, Cedar Park, and Pinehurst.
University District, Holly Park, and View Ridge are the neighbourhoods with the lowest rankings. 

#### Investigate the worst reviews
![image](https://user-images.githubusercontent.com/83236722/142714837-5db08a3f-02c6-490e-b1a3-0f92facc3b52.png)

#### FINDINGS

It's worth noting that the majority of the reviews with low polarity ratings appear to be written in a language other than English!. Maybe the Sentiment Intensity Analyzer has this limitation.  

The other three reviews appear to be genuine complaints, with users lamenting the lack of A/C and fans, the host's rudeness, construction noise disrupting people's stay, and the place's terrible state, among other things. 


# Question 3 - PRICE PREDICTION
7. Can we forecast a listing's price? What aspects of the listing have the best correlation with price prediction?




## File Descriptions <a name="files"></a>

The analysis performed in order to investigate the dataset, data preparation and wrangling, and the creation of prediction models in order to answer the questions above are all documented in the Jupyter notebook. Markdown cells are included in the notebook to aid in the documentation of the procedures as well as the communication of findings based on each analysis. 

For reference an HTML version of the notebook is also available.

Lastly, the seattle folder contains the dataset from Kaggle (https://www.kaggle.com/airbnb/seattle).
Finally, the dataset from Kaggle(https://www.kaggle.com/airbnb/seattle) is contained in the seattle folder.
 
It consists of three files: 
- calendar.csv: calendar attainability of listings and price
- listings.csv: detail about all the attainability listings
- reviews.csv: listing customer feedback

## Summary Of The Results<a name="results"></a>

The following are among the most major findings from the analysis:

1. The summer months of June through August are considered to be the high season in Seattle, with July being the absolute peak. 
2. The most expensive neighbourhood in Seattle was "Southeast Magnolia," followed by Portage Bay. The best price was Rainier Beach.
3. When I looked into other neighbourhoods and property types, I discovered that the most costly houses are in Portage Bay, followed by residences in West Queen Anne and Westlake. 
4. I was able to map the reviews to their various sentiments of positive, negative, or neutral using Sentiment Intensity Analyzer. I discovered that 97.2 percent of reviews were generally good, with only 1% being negative and 1.8 percent being neutral.
5. By looking at review feelings by neighbourhood, I discovered that Roxhill, Cedar Park, and Pinehurst had the most positive ratings, while University District, Holly Park, and View Ridge had the least.
6. Sentiment Intensity Analyzer combines non-English reviews with negative sentiments, which I discovered while investigating the worst reviews. 
7. I was capable of predicting price based on a prepared and cleaned dataset using Linear Regression, with a r2score of 0.62 on both the training and test datasets.
8. It was discovered that a combination of host characteristics and descriptive information about the listing had the greatest effect on the price.

### Blog on Airbnb-Seattle-udacity-project
I have written a blog on website Github Page about the project and observations. Link is down below
https://abdishakury.github.io/

## Acknowledgements<a name="acknowledgements"></a>

Kudos to AirBnB for uploading the dataset and Kaggle for hosting it; the dataset can be found here: https://www.kaggle.com/airbnb/seattle

SentimentIntensity Analyzer Reference: https://www.nltk.org/api/nltk.sentiment.html

Heatmap Reference: https://seaborn.pydata.org/generated/seaborn.heatmap.html
