![dogs](https://user-images.githubusercontent.com/83236722/162843043-eb598134-9bf3-40dc-b03a-6cd2aec95016.PNG)


# Wrangle and Analyze Data
## Introduction
Real-world data rarely comes clean. Using Python and its libraries, I will gather data from a variety of sources and in a variety of formats, assess its quality and tidiness, then clean it. This is called data wrangling. I will document my wrangling efforts in a Jupyter Notebook, plus showcase them through analyses and visualizations using Python (and its libraries) and/or SQL.

The dataset that I will be wrangling (and analyzing and visualizing) is the tweet archive of Twitter user @dog_rates, also known as WeRateDogs. WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because "they're good dogs Brent." WeRateDogs has over 4 million followers and has received international media coverage.

WeRateDogs downloaded their Twitter archive and sent it to Udacity via email exclusively for me to use in this project. This archive contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017. More on this soon.

## What Software Do I Need?

- I need to be able to work in a Jupyter Notebook on my computer. 
- The following packages (libraries) need to be installed. I can install these packages via conda or pip. Please revisit our Anaconda tutorial earlier in the Nanodegree program for package installation instructions.
   - pandas
   - NumPy
   - requests
   - tweepy
   - json

## Project Details
My tasks in this project are as follows:

- Data wrangling, which consists of:
    - Gathering data (downloadable file in the Resources tab in the left most panel of my classroom and linked in step 1 below).
    - Assessing data
    - Cleaning data
- Storing, analyzing, and visualizing my wrangled data
- Reporting on 
      1) my data wrangling efforts and 
      2) my data analyses and visualizations
      
### Gathering Data for this Project
Gather each of the three pieces of data as described below in a Jupyter Notebook titled wrangle_act.ipynb:

 - The WeRateDogs Twitter archive. I was given this file, so imagine it as a file on hand. Download this file manually by clicking the following link: twitter_archive_enhanced.csv

 - The tweet image predictions, i.e., what breed of dog (or other object, animal, etc.) is present in each tweet according to a neural network. This file (image_predictions.tsv) is hosted on Udacity's servers and should be downloaded programmatically using the Requests library and the following URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv


 - I need to be able to create written documents that contain images and I need to be able to export these documents as PDF files. 

# Project Specifications
## Code Functionality and Readability
- All project code is contained in a Jupyter Notebook named wrangle_act.ipynb and runs without errors.
- The Jupyter Notebook has an intuitive, easy-to-follow logical structure. The code uses comments effectively and is interspersed with Jupyter Notebook Markdown cells. The steps of the data wrangling process (i.e. gather, assess, and clean) are clearly identified with comments or Markdown cells, as well.

## Gathering Data
Data is successfully gathered:
- From at least the three (3) different sources on the Project Details page.
- In at least the three (3) different file formats on the Project Details page.

Each piece of data is imported into a separate pandas DataFrame at first.

## Assessing Data
1. Two types of assessment are used:
   - Visual assessment: each piece of gathered data is displayed in the Jupyter Notebook for visual assessment purposes. Once displayed, data can additionally be assessed in an external application (e.g. Excel, text editor).
   - Programmatic assessment: pandas' functions and/or methods are used to assess the data.
2. At least eight (8) data quality issues and two (2) tidiness issues are detected, and include the issues to clean to satisfy the Project Motivation. Each issue is documented in one to a few sentences each.

## Cleaning Data
- The define, code, and test steps of the cleaning process are clearly documented.
- Copies of the original pieces of data are made prior to cleaning.
- All issues identified in the assess phase are successfully cleaned using Python and pandas.
- A tidy master dataset with all pieces of gathered data is created.

## Storing and Acting on Wrangled Data
- Save master dataset to a CSV file.
- The master dataset is analyzed using pandas in the Jupyter Notebook and at least three (3) separate insights are produced.
- At least one (1) labeled visualization is produced in the Jupyter Notebook using Python’s plotting libraries.

#### Hours Vs Retweets
We can see that the number of Retweets is higher at certain times of the day, such as 4 p.m. (16 hours) or 5 p.m. (17 hours).
In contrast, at 3 a.m., 4 a.m., and 1 p.m., the number of Retweets drops dramatically.

![hours_tweet](https://user-images.githubusercontent.com/83236722/162844463-48ce1d46-a488-4078-bb74-0ad323aca7af.jpg)

#### Days of the Week Vs Retweets
Please keep in mind that the numbers 0, 1 and 6 indicate Monday, Tuesday, and Sunday, respectively.
When comparing Saturday and Sunday, we can see that Tuesday and Friday have a better performance in terms of Retweets.

![days_tweet](https://user-images.githubusercontent.com/83236722/162844685-923751ed-0639-47de-b386-fd28298ecde1.jpg)

#### Retweets Vs Dog Breeds
The Breeds with the most Retweets (those with over 23 Retweets over the time range specified in Data Frame) are presented in the above plot.
I observed that different breeds have vastly diverse characteristics. The average retweet count for French Bulldogs is over 2500, while the average 
retweet count for pug toy poddles is less than 1500.

![dog_breading](https://user-images.githubusercontent.com/83236722/162844911-bc87388c-c53b-4e05-987d-5969de516fd5.jpg)

#### Most Common Dog Breed
There are nearly 6000 tweets on WeRateDogs. I was able to examine approximately 1500 tweets. The most popular dog breeds are the **Golden Retriever (143)**, 
**Labrador Retriever (103)**, **Pembroke (94)**, and **Chihuahua (87)**.

![popular_dogs](https://user-images.githubusercontent.com/83236722/162843277-4795ae32-53b3-4fa5-b0df-d7a469bbd63f.jpg)

#### Popularity of Accounts throughout Time
As shown in the graph below, the page grew in popularity over time. The number of favourites seem to be increasing. We might assume that as the **WeRateDog** account 
grew in popularity, tweets were becoming more and more popular.

![popularity](https://user-images.githubusercontent.com/83236722/162843436-800c94ae-5a2c-4b41-98f4-abc5a5e9146b.jpg)

#### Dog types
Dogs are divided into four stages by WeRateDogs: doggo, pupper, puppo, and floof (er). According to the graph below, Pupper is the most common dog group, 
followed by Doggo, and Floofer is quite rare.

![dog_type](https://user-images.githubusercontent.com/83236722/162845411-fdc7cb7b-b127-4792-8c4a-abd631983b18.jpg)

#### Rating Over Time
Lower ratings were more common near the start of the account's activity. With the passage of time, less and fewer dogs obtained a bad rating, while more 
and more obtained a high grade.

![rating_over_time](https://user-images.githubusercontent.com/83236722/162843745-895c2859-1b1b-4813-9798-03e6884df2c8.jpg)

Favorites ratio Vs Retweets

![favourite_tweet](https://user-images.githubusercontent.com/83236722/162845019-09fd2bbd-0e40-4065-a982-546983223f9e.jpg)

## Report
Two reports:
- Wrangling efforts are briefly described in wrangle_report.pdf.
- The three (3) or more insights the student found are communicated in act_report.pdf including visualization.
