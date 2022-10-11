# Amazon_Vine_Analysis
![](/Images/Front.jpeg)
---
## Project Overview
*The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. Here we run analysis on Amazon's Health & Personal Care Review Dataset to determine if there is any positivity bias in reviews written by members of the paid Amazon Vine program.*
____

## Resources
* Software: 
  * [Python, Jupyter Notebook](https://www.python.org)
  * [Google Colab](https://colab.research.google.com)
  * [PostgreSQL](https://www.postgresql.org)
  * [AWD S3](https://aws.amazon.com/ru/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Categories=categories%23storage&trk=ef6eb286-e573-4353-a5b6-197d6ce97d52&sc_channel=ps&s_kwcid=AL!4422!10!71605848472448!71606291145674&s_kwcid=AL!4422!10!71605848472448!71606291145674&ef_id=8ba6bad780921bd325b9d99362b84349:G:s&awsf.Free%20Tier%20Types=*all)
* Data
  * [Health Personal Care](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) 
---

## Results
The first step was to extract the dataset from an AWS S3 using PySpark in order to transform it and load it to AWS again. Please refer to [Amazon_Reviews_ELT.ipynb](https://github.com/DangCoop/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb) to see the code. In this task I use to run the ```GoogleColab```. There, I basically divided the whole dataframe into 4 smaller dataframes for better analysis. These dataframes were then loaded to AWS RDS using a a connection from PySpark to PostgreSQL.

![](/Images/Colab_Customer.png)
![](/Images/Colab_Product.png)
![](/Images/Colab_review.png)
![](/Images/Colab_Vine.png)

Due to the size of the dataframes it took some time to load to PostgreSQL and the RDS. I then did a few quick queries to check that everything ran correctly.
![](/Images/Postg_Customer_tbl.png)
![](/Images/Pg_Custom.png)
![](/Images/Postg_Product_tbl.png)
![](/Images/Pg_Product.png)
![](/Images/Postg_Review_tbl.png)
![](/Images/Pg_Review.png)
![](/Images/Postg_vine_tbl.png)
![](/Images/Pg_Vine.png)


And lastly, I worked with the last table called vine_table to perform the Vine program analysis to filter the best reviews, and see if there were significantly more 5-star reviews in the paid and incentivized (vine) program. The best reviews were those that were highly voted as helpful. Then, I filtered to see which of those were part of the vine program and which were not. Please refer to the [Amazon_Vine_Analysis](https://github.com/DangCoop/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb)

1. *We filtered the dataset down to reviews with more than 20 votes to focus our analysis on the most popular reviews. We then filtered the resulting reviews to those who received a helpful rating greater than or equal to 50%. This resulted in 42 452 reviews for our data set.*
![](/Images/NV.png)

2. *Of the helpful reviews, only 30 are paid Vine Program reviews. With non-Vine reviews making up 42 422 of the dataset:*
![](/Images/Paid.png)
![](/Images/Unpaid.png)   

3. *In the vine rewies there are 14 reviews with 5 star rating, accounting  46.67%% and 22 237 with 5 star rating in the non-vine (unpaid) dataset, accounting 52.42%%.*
![](/Images/StarReview.png))
![](/Images/5star.png)
---

## Summary
There is no evidence to suggest that the Vine reviews contain any positivity bias. Non-Vine reviews make up over 99% of the reviews in the data set and also account for 52.42% of the 5 star reviews. The Vine reviews only have a 5 Star percentage of 46.67%.

### Additional Analysis
![](/Images/Additional.png)

After additional analysis, we can see that there is a slight difference of 0.23 in the average rating of reviews in favor of the vine program. However, there is still not enough information to register in it. A great recommendation would be to apply NLP sentiment analysis to check the words used in most of the reviews. This way we could see more touching and detailed feedback on the vine that we can feel like there is an incentive for customers to leave great reviews.

![](/Images/Back.jpg)

```Denis Antonov 10/10/2022```

```Contact: antonov.resu@gmail.com```