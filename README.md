# DATA 512 - Project Part 1 - Common Analysis
## Wildfire Analysis for Palmdale, California
### Baisakhi Sarkar, Master of Science in Data Science at University of Washington 2023-2025


**❗Important Note: The starting dataset named USGS_Wildland_Fire_Combined_Dataset.json could not be uploaded to git since it is 2.17GB and even after compresion it is 700Mb. But locally that is placed inside the Data folder and used (from local) in the Wildfire_Analysis_Data_Acquisition.ipynb using relative path. The dataset was fetched from [Combined Wildland Fire Datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)**

### Project Goal

More and more frequently summers in the western US have been characterized by wildfires with smoke billowing across multiple western states. There are many proposed causes for this: climate change, US Forestry policy, growing awareness, just to name a few. Regardless of the cause, the impact of wildland fires is widespread as wildfire smoke reduces the air quality of many cities. There is a growing body of work pointing to the negative impacts of smoke on health, tourism, property, and other aspects of society.

The objective of this analysis is to examine wildland fires within a 650-mile radius of Palmdale, California, over the past 60 years (1964-2020). Based on this data, a smoke estimate is developed to assess the impact of wildfire smoke. This estimate is then used to build a predictive model to forecast potential smoke impacts for the next 30 years (through 2050). The ultimate goal of this analysis is to provide actionable insights to policymakers, city managers, councils, and other civic institutions to help them determine whether and how they should implement strategies to mitigate the future effects of wildfires.

### Datasets Used

The source dataset for this analysis is the [Combined Wildland Fire Datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81) dataset. This dataset, compiled and maintained by the U.S. Geological Survey (USGS), provides comprehensive historical wildfire data. It is well-documented and offers fire polygons in both ArcGIS and GeoJSON formats, enabling detailed geospatial analysis.

### API and Documentation
Air quality data was required to assess the performance of the smoke estimate created. This data was obtained from the [US Environmental Protection Agency (EPA) Air Quality Service (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html). The AQS API provides historical air quality data but does not support real-time monitoring. The [API documentation](https://aqs.epa.gov/aqsweb/documents/data_api.html) offers detailed descriptions of various parameters and examples of API calls.

The US EPA was established in the early 1970s, but standardized monitoring with quality assurance procedures only began in the 1980s. As a result, many counties have air quality data starting between 1983 and 1988, while some counties still lack monitoring stations.
The AQS API resolves this limitation by offering search functionalities for monitoring stations and data. Users can query the API using station IDs, county designations, or geographic bounding boxes.

Additional details about the Air Quality System can be found in the [EPA AirData FAQ](https://www.epa.gov/outdoor-air-quality-data/frequent-questions-about-airdata).

### Intermediate Data Files: 

During the course of this study, mainly three intermediate data files were created (two other redundant files are also generated but not used later for analysis):

**Past_60_years_wildfires_with_distances_from_Palmdale.csv**
This CSV file contains data on all wildfire instances spanning the years 1964 to 2020.

**Yearly_AQI_Data.csv**
This CSV file stores the maximum AQI values for each fire season (from May 1st to October 31st) on an annual basis for Palmdale, California.

**Final_Wildfire_Data_Cleaned.csv**
This cleaned dataset was created by removing irrelevant columns, filtering out wildfires which are more than 650 miles away from Plamdale, California. The resulting dataset contains 45,891 rows and 9 columns.

### Known Issues or Assumptions:

Both the Wildfire and AQI datasets used in this analysis were developed based on several key assumptions to ensure consistency and relevance to the study objectives. Below are the key assumptions and the rationale behind them:

**1. Fire Season Definition:**
The fire season was defined as the period from May 1st to October 31st each year. This time window reflects when most wildfires occur and when their impact on air quality is most significant.

**2. Maximum AQI as Annual Estimate:**
For each fire season, the maximum AQI value was selected to represent the AQI for that year. This assumption aligns with the focus of this study, which is to capture the most extreme pollution events likely driven by wildfire smoke.
Using the maximum AQI ensures that high-impact pollution incidents, which can have the most adverse effects on public health and air quality, are not overlooked.

**3. Missing Data Handling:**
AQI data was only available for select years, with many counties having incomplete or no monitoring data prior to the 1986. In such cases, AQI estimates are only reported when available, and missing years were not imputed to avoid introducing bias.

**4. No Exogenous Variables:**
Although factors like wind direction, humidity, and temperature influence smoke dispersion, they were not included in the model due to data unavailability for the entire study period.
These assumptions were made to maintain consistency across datasets, ensure data quality, and focus on the extreme pollution events most relevant to policymakers and public health officials.

### Results

Three visualizations were generated which have been stored in the directory:
1. Histogram of the distribution of wildfires by their distance, upto 1800 miles from Palmdale, California
2. Line graph of the total acres burned by wildfires every year
3. Time series graph containing the cumulative smoke estimate and the maximum AQI estimate for every year

### Research Implications:

This project provided valuable insights into the magnitude and frequency of wildfires across the U.S. over the past 60 years, highlighting their impact on air quality and the importance of wildfire data in environmental analysis. Additionally, it introduced me to GeoJSON files—a new data format—and enhanced my skills in working with geospatial data.
From a sustainability perspective, this project was not only informative but also engaging, as it felt like uncovering hidden patterns in wildfire behavior. Each step—whether building the smoke estimate from scratch, experimenting with different feature combinations, or refining the model—was challenging but highly rewarding. The iterative process of selecting and testing various features provided deeper insight into the complexity of wildfire impacts and the role of data-driven decision-making.

The modeling phase proved to be the most challenging, requiring the exploration of several models to identify one that could effectively handle data with frequent peaks and dips in the absence of reliable predictors. Eventually, the moving average model emerged as a suitable choice, reinforcing the importance of adaptive techniques in time series forecasting. This project not only broadened my understanding of different modeling approaches but also emphasized the need for flexibility and creativity when dealing with noisy environmental data.
Overall, the project enhanced my knowledge of data analytics, sustainability, and time series modeling, while equipping me with practical tools for addressing real-world environmental challenges.
