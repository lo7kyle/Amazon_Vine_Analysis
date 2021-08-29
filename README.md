# Amazon_Vine_Analysis
Create an ETL using PySpark, AWS, and pgAdmin

## Overview:
In this challenge we are given the task to use pyspark to perform an ETL on Amazon product Reviews. I created an ETL that connected to an AWS RDS instance in my PostgreSQL.  

## Purpose:
The purpose of this challenge is to introduce the ETL process to big data pipelining. To interface with the cloud service of AWS and the Big Data, I had to use Apache Spark. Spark is an engine that combines a multitude of large-scale data processing capabilities accessible in multiple languages. In my case I used the python-based spark, Pyspark. The goal here is to take the Amazon product review from an S3 bucket on the AWS and perform a basic pipelining that will create multiple useful tables to store on our pgAdmin SQL database. I then took one of the tables and did a quick analysis to see if the Amazon Vine program for paid reviews had any review bias.     

## Resources
* Data Source: (amazon_reviews_us_Electronics_v1_00.tsv.gz)
[Link to Data Source](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Electronics_v1_00.tsv.gz)
* Software: 
PostgreSQL 11, 
Google Colaboratory,
Spark Version: http://www.apache.org/dist/spark/$SPARK_VERSION/$SPARK_VERSION-bin-hadoop2.7.tgz


## Analysis:
### Overview of Analysis:
When manipulating and using big data an ETL pipeline is a must have. In this analysis there is about a 2Gb .tsv file of reviews with many columns. With too much data to look at it is much harder to perform an analysis. This is where the ETL process comes in. First, we Extract the data from the S3 bucket, then we transform the data by cleaning and separating the data into bite size tables to do our analysis, and finally we load the tables into a database so we can do further analysis and share our findings.   

### Results:
The results can be seen in the .ipynb files. Unlike extracting data from multiple sources and from different sources, we only had one source of data to work with. With smaller data we can expect our data set to need a lot more cleaning, this data set of reviews however was a big file but didn't need as much cleaning. The idea here was more so to separate the data into smaller tables to create relations between them and do our analysis this way. For best practice, it is always good to have a customer’s table with the customers id and a products table with products id. From these two main tables we can create a relation with the review table. 

See below for the tables created through the transformation process:

![Customers_table](https://github.com/lo7kyle/Movies-ETL/blob/main/Resources/Ratings%20import%20count.PNG) 

![Product_Table](https://github.com/lo7kyle/Movies-ETL/blob/main/Resources/movies_df%20import%20count.PNG) 

![Vine_Table](https://github.com/lo7kyle/Movies-ETL/blob/main/Resources/movies_df%20import%20count.PNG) 

From our analysis we wanted to know if the paid Vine Reviews program had any bias in their reviews, meaning the paid reviews had higher ratings than that of unpaid reviews. For this analysis I only looked at 5-star reviews. We can also make a case for 4-star reviews because someone is more likely to give a 4-star review instead of a 5 star review. The results I can honestly say wasn't surprising, but this showed that there isn't any bias in paid reviews. We see that there are more unpaid reviews than the paid reviews. Looking below we also see that there is a lower 5-star percentage from the paid vine reviews than the unpaid. I can assume that this is due to the process of having someone reach out to the customer for review will give a more honest opinion on the product than someone who is reviewing the product on their own.  

![Vine_Analysis](https://github.com/lo7kyle/Movies-ETL/blob/main/Resources/movies_df%20import%20count.PNG) 

There are many analyses we can do on these reviews such as sentiment analysis or even screening for bots, but for a quick way to perform an analysis for bias quick math is always a good way to start. 

### Summary:
Looking at our results we can say for now that there are no signs of positivity bias for reviews in the Vine program. As mentioned in the results this can be due to an interaction between the program and the product itself. I am taking an approach as if the waiter comes to your table and ask if your food is ok or if you are doing well. We tend to be more honest if we need an adjustment in the meal than if a waiter isn't present at all. I understand that this can also work inversely which is why further analysis must be done. Another analysis I wanted to perform was doing this on 4-star ratings. We can assume that there are more 4-star ratings than that of 5-star ratings. This might give a more accurate picture of the bias in reviews. Mentioned earlier was also bot screening since many companies have bot farms that write up fake reviews for a product. This service like the Vine program is then sold to the companies of the products to boost up sales.
