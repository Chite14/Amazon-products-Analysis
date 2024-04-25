# Analysis

## Table of contents

- [Project overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools used](#tools-used)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results and Findings](#results-and-findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)


## Project overview

In this project we are analysing sales of particular products on Amazon from a dataset made in the kaggle data science enviroment. It is an amazing dataset to work with as it wil give us the key performance indicators necessary for the growth of different shops. We will be using python with pandas to clean the data, and give more insight on the sales, ratings etc.

## Data Sources

[Download DataSet](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)
This dataset is having the data of 1K+ Amazon Product's Ratings and Reviews as per their details listed on the official website of Amazon.

Features

• product_id - Product ID

• product_name - Name of the Product

• category - Category of the Product

• discounted_price - Discounted Price of the Product

• actual_price - Actual Price of the Product

• discount_percentage - Percentage of Discount for the Product

• rating - Rating of the Product

• rating_count - Number of people who voted for the Amazon rating

• about_product - Description about the Product

• user_id - ID of the user who wrote review for the Product

• user_name - Name of the user who wrote review for the Product

• review_id - ID of the user review

• review_title - Short review

• review_content - Long review

• img_link - Image Link of the Product

• product_link - Official Website Link of the Product



## Tools used
- Clean data using python with pandas using jupyter notebook. [Download here](https://anaconda.com)
- After cleaning of data we used seaborn visualization to give insights on the data for report. [Read Documentation here](https://seaborn.pydata.org/)
- Data saved into excel from python for easy access

## Data Cleaning and Preparation
1. Data Loading and Inspection
2. Handling missing values
3. Data Cleaning and Formatting

## Exploratory Data Analysis

EDA involved exploring the sales data to answer the key questions;

1. What is the top 8 highest and lowest category rating count?
2. which products have the highest rating?
3. what periods had peak sales, made most money?
4. Which products had the least ratings?

## Data Analysis

In Our Data Analysis we are using Jupyter Notebook, to code in python using pandas. as seen in the code belowe we start by importing pandas which is a library that I downloaded in Anaconda, as well as matplotlib which is a library for visualization, seaborn another library for visualization and in the data cleaning we imported regrex as re used for cleaning symbols or objects out of data. To run this code in your browser you can open this link [Google Colab](https://colab.new/)

```python
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
import re
print("Setup Complete")

data_url = r"C:\Users\Chitemwiko\OneDrive\Documents\amazon.csv"

amazon_data = pd.read_csv(data_url,index_col="product_id")

amazon_data.head()

amazon_data.isnull().sum()

amazon_data.fillna(method='bfill',axis=0).fillna(0,inplace=True)

amazon_data.isnull().sum()

amazon_data.dtypes

amazon_data['discounted_price'] = amazon_data['discounted_price'].str.replace('₹','')
amazon_data['actual_price'] = amazon_data['actual_price'].str.replace('₹','')
amazon_data['discounted_price'] = amazon_data['discounted_price'].str.replace(',','')
amazon_data['actual_price'] = amazon_data['actual_price'].str.replace(',','')
amazon_data['discount_percentage'] = amazon_data['discount_percentage'].str.replace('%','')
amazon_data['rating_count'] = amazon_data['rating_count'].str.replace(',','')
amazon_data

amazon_data.dtypes

amazon_data['discounted_price'] = amazon_data['discounted_price'].astype('float')
amazon_data['actual_price'] = amazon_data['actual_price'].astype('float')
amazon_data['discount_percentage'] = amazon_data['discount_percentage'].astype('float')
amazon_data['rating_count'] = amazon_data['rating_count'].astype('float')

amazon_data.dtypes

amazon_data.tail()

category = amazon_data.groupby(['category'], observed= True)['rating_count'].sum().sort_values().head(10)
category

category.plot(kind="barh", fontsize=6)

Data Shows that the category with the highest no. of ratings is Home & Kitchen in top 3 whilst Office Products comes in fourth place.



category_ = amazon_data.groupby(['category'], observed= True)['rating_count'].sum().sort_values()

category_.nlargest(8)

category_.nsmallest(8)

category_small = category_[category_<480]

category_large = category_[category_>319000]

small_s = pd.Series([category_small.sum()], index =["Other"])

category_large = category_large.append(small_s)

category_large.plot(kind='pie', title ="Sample of Category Data with Largest top 8 Rating Count with Other being the smallest Rating Count",fontsize=15,labeldistance=None, figsize =(10,10)).legend(bbox_to_anchor =(1.5,1),fontsize=15)


```

## Results and findings
- Highest rating means that products haven't met customers full satisfaction.
- We can see from the data that Home anf Kitchen appliances are the most sort after products and has the highest ratings followed by Office supplies, with Electronics being the least rated products.
- 


## Recommendations
actions company needs to make based on analysis


## Limitations

- The category column given the length of the string cannot be cleaned using .str.split() method. 
The scope of the category column makes it difficult to give the largest and smallest rate count, given we cannot determine the average of each category as a whole.
- This data set is mainly about user experience on the product itself, it leaves out information on the seller and delivery satisfaction. 


## references
1. [Kaggle data set](https://kaggle.com)
2. [seaborn: statistical data visualization](https://seaborn.pydata.org/)


