# Data Nation
## Overview: For this project, we are working with PowerSportsNation, a power sports dealer located in Nebraska. PowerSportsNation provides quality used parts that are cheaper than retail. They have asked us to analyze their data for trends and provide possible business recommendations.

### Purpose: The purpose of this analysis is to analyze PowerSportsNation data to identify trends in the sales and marketing, as well as provide possible business recommendations. 

We chose to work with PowerSportsNation because it provides our team an opportunity to work with real world data and provide true solutions/recommendations to improve a company.

## Questions to answer: 
1. What are the demographics and behaviors of customer segmentation? Can we develop marketing personas?

    1. a. Who are our core dealers/customers that the company should be reaching out to for business?

    1. b. How much do one time purchasers provide to the company?

### Tools used for this analysis: Jupyter Notebook, SQL, Python, Pandas

## Analysis
PowerSportsNation (PSN) provides used parts that are typically cheaper than retail. However, they are unaware of their customer segmentation, or target audience or segment for example. By assisting PSN understand their customer segmentation, we can provide them insight into specific groups that buy their parts based on demographics and behaviors.

There are five areas where we need to collect data from in order to analyze customer segmentation: [customer sales](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/sales_info.csv), [customer sales brand total](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/CustomerBrandTotals.csv), [customer sales line of business (LOB) total](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/CustomerLOBTotals.csv), [customer demographics](), and [zip code demographics](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/USZip_Info.csv). From the customer sales information though, we wanted to include recency, frequency, and monetary (RFM) customer enhancement information, creating a new dataset, [RFM Data](https://github.com/ranmacmo/DataNation/blob/a5baac617074644c94c11a038b520eb5c300ef63/data/rfm_data.csv). For this analysis, we are looking at demographics and behaviors for customer segmentation. The brand data and LOB data both provide information for behaviors, while the customer and zip code data provide the demographic information. 

Due to data access restrictions, Randy was in charge of getting the data, cleaning the data, and removing any identifiable information about customers. Then all the datasets will be merged together on the zip code to provide the team with one dataset with all the combined information required to run our analysis. 

## Challenges
One challenge we have faced so far is the limitations the team has to the data. Randy works for PSN so he is able to access the information and data to provide to the team, but most of the cleaning and table creations have to be completed by Randy through their company's SQL package. 

Another challenge we faced with the data was merging the data sets together. Morgan tried to merge the data using Jupyter Notebook, Pandas, and Python, but due to issues we were having with the data, Randy needed to merge the data in the company's SQL package. 

## Limitations
There are also some limitations to this analysis. One limitation is our data is dependent on the company/employees entering all the data information required/needed to run the analysis. Otherwise, it leaves us with NA's scewing our data or causing potential errors when running analysis. 

Another limitation is the data is dependent upon other sources as well such as Amazon and ebay. This is because they also need provide all the data we need from sales that are made on their websites compared to PSN's actual website.