# UW_MSDS_Data512_Au23_Project

### Part I: Common Analysis

*Preparation for Datasets*

1) WildFire Dataset
  obtained from [website]()
2) AQI Dataset
  obtained from [API (documentation)]()

*Preprocessing of Datasets*

**WildFire Dataset**

1) Filtered the dataset with dates from 1963 to 2023
2) Used the biggest ring and the latitude and the longitude of the city and calculated the distance from the center of the city and the center of the biggest ring of the fire
3) Used to calculated distance to filter out the fires that are within 1250 miles radial


**AQI Dataset**

1) Requested an account and looked up using the FIPS code of the city
2) Defined bounding box after it was found that no monitors are around the city
3) Scale-1 bounding box did not work
4) Scale-2 bounding box returned 4 sites, while the one started the earliest was in 2000
5) Scale-3 bounding box returned a few sites with start-dates in 1988

*Estimation of AQI*


