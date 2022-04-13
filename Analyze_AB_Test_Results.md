# Analyze A/B Test Results

## Introduction:

For this project, we will work to understand the results of an A/B test run by an e-commerce website. The company has developed a new web page in order to try and increase the number of users who "convert," meaning the number of users who decide to pay for the company's product. Our goal to help the company understand if they should implement this new page, keep the old page, or perhaps run the experiment longer to make their decision.

A/B tests are very commonly performed by data analysts and data scientists. 

For this project, the results of an A/B test run by an e-commerce website.
- The company has developed a new web page in order to try and increase the number of users who "convert," meaning the number of users who decide to pay for the company's product. 

My goal in this notebook is to help the company understand if they should implement the new page, keep the old page, or perhaps run the experiment longer to make their decision.


![boostrapping](https://user-images.githubusercontent.com/83236722/162836086-fe565948-9ca9-444e-8d53-4885f6abc9d3.jpg)



## Software:

One can do this project in Jupyter Notebook. For doing this project one has to install the following packages -
- Pandas
- Numpy
- Matplotlib
- Statsmodels

## Project Steps:

### Data Wrangling:

- remove duplicates or records with missing or mismatched values
- handle the rows where the landing_page and group columns don't align

### Data Analytics:

- Compute probabilities of converting: 
    - regardless of page
    - Given that an individual received the treatment
    - Given that an individual received the control page
- Perform Hypothesis Testing and calculate p-values
- Conduct Logistic Regression


![hist_Pvalue](https://user-images.githubusercontent.com/83236722/162835729-b5c46ec4-252b-4ada-b4f5-f375854f70b4.jpg)


![PartII_ab_test](https://user-images.githubusercontent.com/83236722/162835750-beb935ef-e640-46c0-a06b-f901bb78f41f.jpg)

![table](https://user-images.githubusercontent.com/83236722/162835766-e4efc807-8ba0-440d-93f5-350ca60d6dda.jpg)


# NoteBook Content


Part I - Probability

Part II - A/B Test

Part III - A regression approach

![logistic_regression](https://user-images.githubusercontent.com/83236722/162836359-fcd3a734-3692-4c5e-a2aa-f5ed851f1676.jpg)


## Conclusions

The findings show that the new and old pages have roughly equivalent chances of converting users, based on the statistical tests we conducted, the Z-test, logistic regression model, and actual difference identified. The null hypothesis is not rejected. I advise the e-commerce business to retain the old page. This would save you time and money by avoiding the need to establish a new website.
