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

![Fire_Counts_in_Range](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/ad9b035b-be89-4fcd-9134-dcb8b8efe08d)

The graph shows that there are more fires at further distances.

![Acres_Per_Year](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/bd7a40b2-ed27-4ca5-8591-3dde85622c1d)

This graph shows that there is likely a trend that there are more and more acres burned each year since the general direction is going upward.

![Comparison between EstAQI and AvgAQI](https://github.com/hww1999/UW_MSDS_Data512_Au23_Project/assets/50925030/ffd49411-4abc-4c35-8442-af6945fefed7)

This graph shows the comparison between the gaseous AQI from site 35013 and the AQI produced by eistimation using GIS_Acres and average distance from the center of the fire to the center of the city.

