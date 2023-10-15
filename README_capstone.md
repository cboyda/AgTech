# Project: AgTech Capstone
Final Project | Cohort 4 | Stream 3 by Clinton Boyda

## Problem Statement
Reviewing crop prices, I was intrigued to see the Canola drastically increasing:
![Canola Pricing](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/CanolaPrices.png)

I was curious, if a rural municipal district has a high yield, how would that compare to its value? 
I assumed the top crop yield RMs would also have the highest valuation.

## Project Goals
This sample challenge is to go shopping for the best canola-valued rural municipal locations.  Value will be calculated by taking the crop yield x stock crop price.

![Canola Valuation Function](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/canola_function.png)

## Data Process
### Step 1: Crop Data

* Incorporate RM yields for numerous crops from both Saskatchewan and Manitoba
* 8 Crop yields included for crop_columns=['Canola', 'Barley', 'Canary Seed', 'Durum Wheat', 'Lentils', 'Oats', 'Spring Wheat', 'Peas']
* 397 Total Rural Municipalities (RM) for both Saskatchewan (SK) and Manitoba (MB)
* 1938 - 2022 Complete Timeline of Data Gathered
* Due to missing values Canola crop yield data was limited to 2002-2022
* Manitoba Yields converted from tonnes to bushels
* Saskatchewan converted from pounds to bushels
* Source: [Saskatchewan Data](https://dashboard.saskatchewan.ca/agriculture/rm-yields/rm-yields-data) and [Manitoba Data](https://geoportal.gov.mb.ca/search?collection=Dataset&q=crop%20yields)

### Step 2: Gather GIS Data

* Incorporate Geospatial data for each of RM's from provinces
* RM data was missing for the SK RM's 278, 408, and 529 and MB RM's UNORG TERRITORY, luckily these don't appear in our top 10 list so this missing data can be ignored for this analysis.
* 478 Total Rural Municipalities (RM) have shape files available for SK and MB (3 duplicates)
* Source: Shapefiles provided

### Step 3: Gather Canola Pricing

* Grab Canola stock prices
* 3285 daily Stock prices found for Canola as $ per Tonne and **$ per Bushel** (selected) (averaged for each year)
* Data was limited to 2010-2022
* Source: [investing.com](https://www.investing.com/commodities/canola-futures-streaming-chart)

### Step 4: Methodology: Partitional Clustering
Utilized unsupervised learning.

| Step                          | K-means | DBSCAN |
|-------------------------------|---------|--------|
| Feature Engineering            |   Yes   |   Yes  |
| Data Splitting for Training   |   No    |   No   |
| Model Selection               |   No    |   No   |
| Removed Crop Outliers         |   No    |   No   |
| Data Preprocessing            |   Yes   |   Yes  |
| Parameter Selection           |   Yes   |   Yes  |
| Cluster Evaluation            |   Yes   |   Yes  |
| Scalability                   |   Yes   |   Limited  |
| Cluster Interpretability      |   Yes   |   Moderate  |

<details>
  <summary>ANALYSIS DETAILS... [click to view]</summary>
  
#### K-Means
K-means is a partitioning-based clustering algorithm. It assigns data points to clusters by minimizing the sum of squared distances between data points and the centroid of their assigned cluster. It assumes that clusters are spherical and equally sized.

#### DBSCAN
DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is a density-based clustering algorithm. It defines clusters as dense regions of data points separated by areas of lower density. It doesn't assume spherical clusters and can discover clusters of arbitrary shapes.

</details>

# Results
Highlight any strengths or weaknesses??? End with Conclusion: Summarize the key takeaways from the project, and discuss the implications and potential applications of the results. Provide recommendations for future work.
### a) Model Comparison

### b) Exploratory Data Analysis (EDA)

### c) Insights

## Data Visualizations

## Challenges
* GIS shapefiles were missing for 4 RMs for the best visualization these should be included

## Future Goals
* Better accuracy: use province specific pricing like [Manitoba Canola specific prices](https://geoportal.gov.mb.ca/datasets/manitoba::manitoba-crop-prices-historical/explore) instead of generalizing with stock prices for all locations
