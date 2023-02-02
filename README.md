# [Data Nation](https://github.com/ranmacmo/DataNation/blob/f30f6e80958a11505348b585722381feb6c10620/PSN_Data_Presentation.pdf)
## Overview: For this project, we are working with PowerSportsNation, a power sports dealer located in Nebraska. PowerSportsNation provides quality used parts that are cheaper than retail. They have asked us to analyze their data for trends and provide possible business recommendations.

### Purpose: The purpose of this analysis is to analyze PowerSportsNation data to identify trends in the sales and marketing, as well as provide possible business recommendations. 

We chose to work with PowerSportsNation because it provides our team an opportunity to work with real world data and provide true solutions/recommendations to improve a company.

## About the Data
PSN works with used parts that are sold across the world. To understand customer segmentation we took two years of customer order details per customer, such as customer ID, part brand, the market, and line of business. 

In addition, to better understand customer segmentation, we needed to collect zip code demographics, such as zip code, latitude, and longitude. 

Then we can merge all the data together to get a more comprehensive analysis of customer segmentation based on customer behavior and location demographics.

## Questions to answer: 
1. What are the demographics and behaviors of customer segmentation? Can we develop marketing personas?

    1. Who are our core dealers/customers that the company should be reaching out to for business?

    1. How much do one time purchasers provide to the company?

### Tools used for this analysis: Jupyter Notebook, SQL, Python, Pandas

## Analysis
PowerSportsNation (PSN) provides used parts that are typically cheaper than retail. However, they are unaware of their customer segmentation, or target audience or segment for example. By assisting PSN understand their customer segmentation, we can provide them insight into specific groups that buy their parts based on demographics and behaviors.

There are five areas where we need to collect data from in order to analyze customer segmentation: [customer sales](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/sales_info.csv), [customer sales brand total](https://github.com/ranmacmo/DataNation/blob/cfd4aa9a765c0e57ea30c35859dccf23be4f0d86/data/Customer_brands.csv), [customer sales line of business (LOB) total](https://github.com/ranmacmo/DataNation/blob/cfd4aa9a765c0e57ea30c35859dccf23be4f0d86/data/Customer_lob.csv), [customer demographics](https://github.com/ranmacmo/DataNation/blob/cfd4aa9a765c0e57ea30c35859dccf23be4f0d86/data/Customers.csv), and [zip code demographics](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/USZip_Info.csv). From the customer sales information though, we wanted to include recency, frequency, and monetary (RFM) customer enhancement information, creating a new dataset, [RFM Data](https://github.com/ranmacmo/DataNation/blob/cfd4aa9a765c0e57ea30c35859dccf23be4f0d86/data/Customer_rfm.csv). For this analysis, we are looking at demographics and behaviors for customer segmentation. The brand data and LOB data both provide information for behaviors, while the customer and zip code data provide the demographic information. 

Due to data access restrictions, Randy was in charge of getting the data, cleaning the data, and removing any identifiable information about customers. Then all the datasets will be merged together to provide the team with one dataset with all the combined information required to run our analysis, Image 1. 

### Image 1: Process Flow Diagram
![Diagram](https://github.com/ranmacmo/DataNation/blob/92ee47321a4fce4a1828bc57ea650bcca0143cd2/images/Process%20Flow.png)

The best way to merge the datasets together is on the Customers dataset, Image 2. 

### Image 2: Customers DataFrame
![Customers Dataset](https://github.com/ranmacmo/DataNation/blob/f3f79096459f30ca11785ff1903a1effcad94f1b/images/customers_df.png)

Then, we merged each indivdiual dataset to the customers dataset. First, we merged the customer brands dataset to the customers master dataset, then we merged the customers LOB dataset, customers market dataset, RFM dataset, and lastly the demographic dataset. When merging the brands, LOB, marketing, and RFM datasets to the master customers dataset, we merged them on Customer ID. However, for the demographic information we had to merge them together on the zip code. 

When we started with the customer dataset, we had a total 141,461 total rows and 3 columns. However, after merging all the datasets together, we ended up with a total of 140,533 rows and 39 columns, Image 3.

### Image 3: Merged Dataset
![Merged Dataset](https://github.com/ranmacmo/DataNation/blob/f3f79096459f30ca11785ff1903a1effcad94f1b/images/merged_data.png)

# Description of the data exploration phase of the project
Once the data was merged together into one [dataset](https://github.com/ranmacmo/DataNation/blob/f4ecc2501f44d0fd0079ed439820d95423f9e387/data/Customer_data_merged.csv), we still needed to make some adjustments before we could compute the machine learning. Since we didn't need all the columns for machine learning, we created a new DataFrame containing only the following columns: Recency, Frequency, Monetary, Market Website total, and Market eBay total. Table 1. 

### Table 1
![new_data_df](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/new_data_df.png) 

Now that we have our variables we want to run the machine learning on, we needed to normalize the data using the MinMaxScaler() function. After the data was normalized, we could then compute the KMeans function to generate an elbow curve to find the number of clusters needed for the analysis. When we ran the KMeans, our elbow curve indicated two clusters, Image 4. 

### Image 4: Elbow Curve
![Elbow Curve](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/elbow_curve.png)

Now that we know how many clusters we have, we calculated the predicted values and combined the predictions with the dataset, Table 2. 

### Table 2
![data_df_scaled](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/data_df_scaled.png)

Lastly, we can run a pairplot to compare the values between one another to visually see the clusters, Image 5. However, after computing the first pairplot, we decided to re-run the analysis using 3 clusters instead of 2, to see if their were additional clusters we might be missing, Image 6. 

### Image 5: 2 Cluster Comparison
![2 cluster comparison](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/two_cluster.png)


### Image 6: 3 Cluster Comparison
![3 cluster comparison](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/three_cluster.png)

Looking at the cluster comparisons, you can see that there is signitficant clustering between Recency and the other variables. Indicating there were two signifcant groups for Recency on each variable. 

# Description of the analysis phase of the project
Now that we have a little better understanding of the data, we decided to add in additional columns and run the machine learning again. This time, we added in all the brand total columns to add for the machine learning analysis. Then we scaled the data and ran another KMeans elbow curve, Image 7. For this elbow curve, we also increased our K range from (1, 10), to (1, 50) to make sure we have the best range to predict our possible number of clusters. 

### Image 7: Brands Elbow Curve
![Brands Elbow Curve](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/brand_elbow.png)

After running the elbow curve, we concluded there are 4 clusters. Just like we did previously, we calculated the predicting values and combined the predications to the scaled dataset and computed the pairplot, Image 8. After adding in the brands to the machine learning, there was a lot more clustering between the variables. By looking at the comparisons, you can see that Recency still indicates the greatest clustering between the other variables. 

### Image 8: Brands Cluster Comparison
![Brands Comparison](https://github.com/ranmacmo/DataNation/blob/6626a307d3add38a77dd2aa0ee3f07e7c882ac21/images/brands4.png)

For this analysis, we used Jupyter notebook to organize the data and run machine learning for clusterings. 

## Challenges
One challenge we have faced so far is the limitations the team has to the data. Randy works for PSN so he has to pull all the data and remove identiable information before the remaining team can access the data. 

## Limitations
There are also some limitations to this analysis. One limitation is our data is dependent on the company/employees entering all the data information required/needed to run the analysis. Otherwise, it leaves us with NA's scewing our data or causing potential errors when running analysis. 

Another limitation is the data is dependent upon other sources as well such as Amazon and ebay. This is because they also need provide all the data we need from sales that are made on their websites compared to PSN's actual website.