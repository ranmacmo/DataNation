# [Data Nation](https://github.com/ranmacmo/DataNation/blob/75586569058b2fe40f5bac9ad991b390779a0cf9/PSN_Data_Presentation.pdf)
## Overview: For this project, we are working with PowerSportsNation, a power sports dealer located in Nebraska. PowerSportsNation provides quality used parts that are cheaper than retail. They have asked us to analyze their data for trends and provide possible business recommendations.

### Purpose: The purpose of this analysis is to analyze PowerSportsNation data to identify trends in the sales and marketing, as well as provide possible business recommendations. 

We chose to work with PowerSportsNation because it provides our team an opportunity to work with real world data and provide true solutions/recommendations to improve a company.

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

## Challenges
One challenge we have faced so far is the limitations the team has to the data. Randy works for PSN so he has to pull all the data and remove identiable information before the remaining team can access the data. 

## Limitations
There are also some limitations to this analysis. One limitation is our data is dependent on the company/employees entering all the data information required/needed to run the analysis. Otherwise, it leaves us with NA's scewing our data or causing potential errors when running analysis. 

Another limitation is the data is dependent upon other sources as well such as Amazon and ebay. This is because they also need provide all the data we need from sales that are made on their websites compared to PSN's actual website.