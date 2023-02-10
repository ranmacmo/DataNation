# [Data Nation](https://github.com/ranmacmo/DataNation/blob/5412547a9937c7506f05e1c524bbd3830dc118ba/WashU_FinalProject.pdf)
## Overview: For this project, we are working with PowerSportsNation, a power sports dealer located in Nebraska. PowerSportsNation provides quality used parts that are cheaper than retail. They have asked us to analyze their data for trends and provide possible business recommendations.

### Purpose: The purpose of this analysis is to analyze PowerSportsNation data to identify trends in the sales and marketing, as well as provide possible business recommendations. 

### [Tableau Dashboard](https://public.tableau.com/app/profile/randy.machacek/viz/CustomerSegmentation_16747875219150/Dashboard2)

## Background
We chose to work with PowerSportsNation because it provides our team an opportunity to work with real world data and provide true solutions/recommendations to improve a company.

Powersports Nation (PSN) is the largest premier remanufacturing and salvage UTV/ATV parts seller in the US. The company has had substantial growth, growing from two employees to over 80, processing over 40 saveage units a week, and rebuilding over 40 engines in a week. Just this past year, PSN made $14M in revenue. 

However, they are unaware of their customer segmentation or target audience. By assisting PSN understand their customer segmentation, we can provide them insight into specific groups that buy their parts based on demographics and behaviors.

## Approach
PSN primary sells thier parts on either their [website](https://www.powersportsnation.com/) or on eBay. Therefore, we collected our data from the customer sales and census demographic data to compute our analysis. For analysis, we are looking at customer segmentation, to understand the customer groups for PSN and the revenue each group produces. Thus, Randy and I used a combination of RFM (recency, frequency, and monetary) statistical analysis as well as machine learning to answer the following questions and provide recommendations.  

    i. Who are our core customers across the various markets?

    ii. Who are our core customers that the company should be reaching out to for business? 

## About the Data
Customer segmentation organizes groups based on shared characteristics, behaviors, or preferences. For the data, we acquired background data on customers to create customer personas as well as census demographic data. 

The customer sales data we collected, had around 250,000 transactions and 140,000 unique customers. Therefore, we broke down the customer sales information into five different datasets: Customer Master, Customer Master Pivot, Customer LOB Pivot, Customer Brand Pivot, and Customer RFM. The [Customer Master data](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customer_sales.csv) contains all the customer sales information, such as the postal code and order date. From the master sales data, we created a new dataset the [Customer Master Pivot](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customers.csv) which contains only the CustomerID, Zipcode, and State. However, since customers made more than one purchase, their ID's were in the dataset more than once. Therefore, we combined each matching customer ID into one row. The [Customer LOB Pivot](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customer_lob.csv) data contains all the information regarding line of buisness, with each matching customer ID being combined into one row. The [Customer Brand Pivot](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customer_brands.csv) contains the total of each brand that is sold for each customer ID. Similar to the other datasets, we combined matching customer ID's into one row. Lastly, the [Customer RFM](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customer_rfm.csv) dataset contains the recency, frequency, and monetary variables and averages for each customer ID. Along with it's RFM score and how the customer is segmented. For example, customer ID's segmented as "champions" are customers that regularly purchase from PSN and make up a good amount of the companies revenue. Whereas, "hibernating" customers are individuals who might purchase every so often, but not regularly or recently. 

Once we cleaned up all datasets, we then merged all five datasets together on the customer ID, which is why it was so important that we had one row for each customer ID in all the datasets. Therefore, we merged all the datasets to the Customer Masters Pivot dataset, Image 1, to create the [Customer Pivot Summary](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customer_data_merged.csv), Image 2.

### Image 1: Customer Masters Pivot DataFrame
![Customers Dataset](https://github.com/ranmacmo/DataNation/blob/f3f79096459f30ca11785ff1903a1effcad94f1b/images/customers_df.png)

### Image 2: Merged Dataset
![Merged Dataset](https://github.com/ranmacmo/DataNation/blob/f3f79096459f30ca11785ff1903a1effcad94f1b/images/merged_data.png)

Since Randy and I also wanted to look at the zip code demographics to understand better where PSN's highest volume of customers are purchasing from, we also collected census demographic information. We cleaned up the dataset that only the important zip code information we were looking for was included, such as the zip code, city, state, and population. The [zip code data](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/zipcode_demo.csv) was then also merged with the Customer Pivot Summary on the zip code variable. 

### Tools used for this analysis: Jupyter Notebook, SQL, Python, Pandas, Tableau

## Analysis
Randy works with PSN, so he collected all the data that we would need to run analysis. He also cleaned the data to remove any identifiable information about the customers or confidential to PSN. 

### Data exploration phase of the project
Once the data was merged together into one [dataset](https://github.com/ranmacmo/DataNation/blob/9e8f0fa987a7cb065201ffb4ef980572c94a8429/data/Customer_data_merged.csv), we wanted to get a brief understanding of the machine learning on a smaller scale. Therefore, we created a new DataFrame containing only the following columns: Recency, Frequency, Monetary, Table 1. We chose these columns because recency, frequency, and monetary are the main values that help us understand customer segmentation. 

#### Table 1: RFM
![rfm_dataframe](https://github.com/ranmacmo/DataNation/blob/fa3025fba9b85332d552b29881bd4cfe1c78d2d5/images/rfm_dataframe.png) 

Recency is how recent the customers purchased from PSN, frequency is the number of times the customer purchased in a given time period, and monetary is the total amount the customer spent. These variables are typically on a scale from 1 to 5, however, if you look at Image 3, you can see the recency scale is from 5 to 1. This is because we want a lower quartile, indicating the customer has made a recent purchase. Frequency and Monetary, we want higher values though to indicate a greater amount purchased and spent. 

#### Image 3: RFM Ranking
![rfm_ranking](https://github.com/ranmacmo/DataNation/blob/71e0616ad00e27ba47f67507874e0ee564b46af0/images/rfm_data_ranking.png)

Before we ran the machine learning, we normalized the data using the MinMaxScaler() function. After the data was normalized, we then computed the KMeans function to generate an elbow curve to find the number of clusters needed for the analysis. When we ran the KMeans, our elbow curve indicated around two or four clusters, Image 4. 

#### Image 4: Elbow Curve
![Elbow Curve](https://github.com/ranmacmo/DataNation/blob/e1e9ed9ce5a769679b3297bb34043b86d7a93908/images/rfm_elbowcurve.png)

For this analysis, we used 4 clusters. Then we calculated the predicted values and combined the predictions with the dataset, Table 2. 

#### Table 2: Scaled Dataset
![data_df_scaled](https://github.com/ranmacmo/DataNation/blob/83f340fb6e3a1e39bd60a0400e1569d96f40e71d/images/rfm_predictions_table.png)

Lastly, we ran a pairplot to compare the values between one another to visually see the clusters, Image 5. From Image 5, you can see that Recency is the strongest value in indicating groups between frequency and monetary. Suggesting that there are four groups that have made recent purchases that strongly correlate with how frequently those customers purchase from PSN as well as how much they spend. 

#### Image 5: RFM Cluster Comparison
![rfm cluster comparison](https://github.com/ranmacmo/DataNation/blob/6aa00d8a73d0d7cc532378699f1cf814b781be12/images/rfm_machine_learning.png)


### Results of the analysis phase of the project
In addition to the machine learning, we also used [Tableau](https://public.tableau.com/app/profile/randy.machacek/viz/CustomerSegmentation_16747875219150/Dashboard2) to get a greater understanding and visual of the customer segmentation data. In Tableau we were able to take the recency, frequency, and monetary values and divide them between customers that purchase off PSN's website, compared to those that purchase off eBay or other source. This allowed us to see a more visual of which groups of customers are purchasing and how much they make up of PSN's revenue. 

Looking at customers that purchase off PSN's website, their champion customers make up 31% of their revenue, whereas, hybernating customers make up 21% of the total revenue from the website. However, hibernating customers make up 31% of the total customers that purchase of their website, compared to the 7% that are champions, Image 6. 

When you look at the customers that purchase off eBay though, hibernating customers make up 37% of the total customers that purchase off eBay, and 29% of the total revenue. Whereas champion customers only make up 6% of the total customers that purchase off eBay and 13% of the total revenue, Image 7. 

#### Image 6: Website RFM Dollars
![website](https://github.com/ranmacmo/DataNation/blob/585a164acf9baf139e1374b428622a57a85fafef/images/website_percentages.png)

#### Image 7: eBay RFM Dollars
![ebay](https://github.com/ranmacmo/DataNation/blob/585a164acf9baf139e1374b428622a57a85fafef/images/ebay_percentages.png)

Getting a general understanding of which groups provide which total of the customers and revenue, it was important to also take a look at which of the groups expressed the most grouping from our machine learning. Therefore, Randy and I put the RFM data into Tableau, Image 8, to discover our main four groups are: can't lose, hibernating, loyal customers, and champions. 

#### Image 8: RFM Top Segments
![rfm segments](https://github.com/ranmacmo/DataNation/blob/09678960edae5aea2b9905b104b1a342f6bc8ef7/images/rfm_segments.png)

It made since that hibernating, loyal customers, and champions were three of the groups, considering they make up the majority of the customers and sales. However, it was interesting to see the cutomer's can't lose as the forth group. This could be because these are customers that might have been in the other three groups, but due to inactivity of purchasing parts, put them in this category. 

## Recommendations
PSN wants to creat a loyalty program for their customers. This analysis was to provide insight into their customer segmentation and know which groups to target based on their demographics and behaviors. It's important for PSN to keep their top customers, so their champions, loyal customers, new customers, and the hibernating customers. These groups make up the majority of their cutomers and revenue. PSN could create a customer program where customers subscribe to their company to recieve discounts or deals.

By providing customers this potential opportunities, could result in hibernating customers, new customers, and even loyal customers as champions. This is because, if customers subscribe to their customer program, they will be creating reaccuring customers.

Another recommendation is to review their current marketing. EBay, like other third party organizations, take part of the profit when a sale is conducting. Therefore, if PSN can remark to get their website more publicity, customers might start to go on their website more compared to eBay. One suggestion would be to add a buisness card or flyers in the packaging before sending a part to a customer.  

## Challenges
The main challange that Randy and I faced with the PSN data, was cleaning the data and determining either what additional information we need, or that we could remove. When Randy and I started working on the machine learning, we discovered we were having issues with the data. Therefore, Randy would go back to review the data and collect what information we still needed from the company. 

Another challange that Randy and I faced during this analysis is when we tried to run the machine learning to include the different brands. When we ran the Kmeans analysis, we didn't get very many clusters from the elbow curve. Therefore, when we ran the comparison plot, there were not very distinct groups. While we did not get much information from the machine learning on the brands, the brands would be good to look at for future analysis. 

## Limitations
There are also some limitations to this analysis as well. One limitation is our data is dependent on the company/employees entering all the data information required/needed to run the analysis. Otherwise, it leaves us with NA's scewing our data or causing potential errors when running the analysis. The data is dependent upon other sources as well such as Amazon and ebay. These sources also need to provide all the data we need from sales that are made on their websites.

## Future Analysis
Since PSN is still a fairly new company, it would be interesting to take a look at their data since they started. Being able to compare from where they started to where they are now, might provide additional insights on their customers.

Another interesting analysis would be to collect data on common google searches that customers put in their web browser, or how they heard about PSN. If the company is experiencing greater sales on eBay compared to their website, it could be because their website doesn't appear when customers do a google search for auto parts. Understanding why customers purchase from other places and how they found the part they needed, would be beneficial.

## Final Comments
One item Randy and I would have done differently, would be to look into whether customrs had more than one account. It's a possibility that customers could have more than one account or customer ID, which could skew a data. 