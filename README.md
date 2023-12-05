# UW_MSDS_Data512_Au23_Project

### Part I: Common Analysis

**Preparation for Datasets**

1) WildFire Dataset obtained from [website](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
2) AQI Dataset and its documentatoin could be found [here](https://www.airnow.gov/sites/default/files/2020-05/aqi-technical-assistance-document-sept2018.pdf)
4) Code to preprocess wildfire dataset comes from [here](https://drive.google.com/file/d/1qNI6hji8CvDeBsnLDAhJXvaqf2gcg8UV/view?usp=sharing)
5) Code to get access to AQI data comes from [here](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view?usp=sharing)
  

**Preprocessing of Datasets**

*WildFire Dataset*

1) Filtered the dataset with dates from 1963 to 2023
2) Used the biggest ring and the latitude and the longitude of the city and calculated the distance from the center of the city and the center of the biggest ring of the fire
3) Used to calculated distance to filter out the fires that are within 1250 miles radial
4) The processed dataset for the city could be found [here](https://drive.google.com/file/d/1ZDMaTStyK2N215kZe9tSSAifTSfXCAOH/view?usp=drive_link) as the size is too large for github


*AQI Dataset*

1) Requested an account and looked up using the FIPS code of the city
2) Defined bounding box after it was found that no monitors are around the city
3) Scale-1 bounding box did not work
4) Scale-2 bounding box returned 4 sites, while the one started the earliest was in 2000
5) Scale-3 bounding box returned a few sites with start-dates in 1988

**Estimation of AQI**

1) Using the calculated distance and the GIS-Acres of the fire to build an estimator
2) Put that estimator into Prophet model to perform time-series prediction


**Conclusion & Visualization**

*the reflection PDF could be found [here](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/blob/main/Part_1_Common_Analysis/Reflection.pdf)*

![Fire_Counts_in_Range](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/ad9b035b-be89-4fcd-9134-dcb8b8efe08d)

The graph shows that there are more fires at further distances.

![Acres_Per_Year](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/bd7a40b2-ed27-4ca5-8591-3dde85622c1d)

This graph shows that there is likely a trend that there are more and more acres burned each year since the general direction is going upward.

![Comparison between EstAQI and AvgAQI](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/ffd49411-4abc-4c35-8442-af6945fefed7)

This graph shows the comparison between the gaseous AQI from site 35013 and the AQI produced by eistimation using GIS_Acres and average distance from the center of the fire to the center of the city.

### Part II: Extension Plan

**Focus of the Plan**

Understanding that water palys a great part in humans' daily lives and thus the cleaniness matters for the city, this extension plan tends to investigate how wildfires could impact the water system of the city, and whether there is anyway to preserve the water the city is drinking or using. We looked for the Water Quality Index (WQI) of the city and planned to see the correlation between the the index and the estimator we created for smoke impact.

**Preparation for Datasets**

1) [WQI](nmtracking.doh.nm.gov/dataportal/query/Index.html) - instead of a general quality index, we found multiple indexes that quantified the concentration of chemical compounds in the water system that serves more than 35k people in the city. Among all those indexes, we at last chose two, which are Haloacetic Acids (HAAs) and Nitrate (Ni) since both had quarterly data and they go into the water system in different ways.

2) [USGS Water Data for the Nation](nwis.waterdata.usgs.gov/nwis) - the dataset is about the yearly water discharge, namely how much water goes through the city in each year. Originally planning to determine whether the amount of water would affect the concentration of the chemical compounds in the water system, yet due to the low correlation and the missing data in between years, the dataset was not used in the actual model building process.

**Preprocessing of Datasets**

*[WQI data](nmtracking.doh.nm.gov/dataportal/query/Index.html)*

1) changed the 'Quarter' column from 'Jan to Mar' into 'Q1' and so on
2) While wildfire dataset and AQI datasets are both yearly data, we need to change WQI into yearly data as well
3) gave different weights to the concentrations in different quarters for fire seasons. Q1:0, Q2:2/6, Q2:3/6, Q4:1/6
4) summed up the weighted concentration in the year
5) grouped by year

**Implications from the Analysis**

![haas_fit](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/eb5d3411-026c-472d-9f18-3ec5ee1aaa7b)

The fitted simple linear regression model between the WQI estimator and the concentration of HAAs in the water system.

![nitrate_fit](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/c2d085cd-a39f-40ae-8162-6bb4aeb457da)

The fitted simple linear regression model between the WQI estimator and the concentration of Ni in the water system.

**Known Issues**

To begin with, tracking the discharge of water might not fully reveal the effects of it upon the city since there lacks enough data about the water quality of the city to testify. Additionally, while a small volume of water discharge could be due to dryness and fire, a large volume of water discharge might not speak otherwise since its appearance could be due to ice melting or other abrupt surges of water. Such factors might be further included in the whole analysis to rule out the potential effects there.
Additionally, while the dataset of the concentration of chemicals has granularity of quarterly and yearly data, quarterly data might work better for time series data. However, while usually wildfire happens only from May to October, it would be hard to decide for the granularity so that datasets could match. Further, as mentioned above, the quantity of data about concentration of chemicals in local water systems is limited. The small sample makes it harder to validate the hypothesis. If there is chance, the same test should be performed for different cities using the data about wildfires closer to those cities and the data from local water systems.

