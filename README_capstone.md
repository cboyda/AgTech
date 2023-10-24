# Project: AgTech Capstone
Final Project | Cohort 4 | Stream 3 by Clinton Boyda

## Problem Statement
Reviewing crop prices, I was intrigued to see the Canola pricing drastically increasing:
![Canola Pricing](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/CanolaPrices.png)

I was curious, if a rural municipal district has a high yield, how would that compare to its value? 
I assumed the top crop yield RMs would also have the highest valuation.

Interesting how [current crop analysis, from June 2023,](https://www150.statcan.gc.ca/n1/daily-quotidien/230628/dq230628a-eng.htm) connects to this query: "Canola area rises
Farmers reported planting 22.1 million acres of canola in 2023, up 3.2% from the previous year. The greater area may be the result of **relatively favourable prices**.
Farmers in Saskatchewan reported planting 12.4 million acres of canola, up 8.8% from 2022."

## Project Goals
This sample challenge is to go shopping for the best canola-valued rural municipal locations.  
Value will be calculated by taking the crop yield x stock crop price.

![Canola Valuation Function](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/canola_function.png)

## Data Process
### Step 1: Crop Data

* Incorporate RM yields for numerous crops from both Saskatchewan and Manitoba
* 8 Crop yields included for crop_columns=['Canola', 'Barley', 'Canary Seed', 'Durum Wheat', 'Lentils', 'Oats', 'Spring Wheat', 'Peas']
* 397 Total Rural Municipalities (RM) for both Saskatchewan (SK) and Manitoba (MB)
* 1938 - 2022 Timeline of Data Gathered
* Due to missing values Canola crop yield data started off being limited to Years 2002-2022
* Manitoba Yields converted from tonnes to bushels
* Saskatchewan converted from pounds to bushels
* Source: [Saskatchewan Data](https://dashboard.saskatchewan.ca/agriculture/rm-yields/rm-yields-data) and [Manitoba Data](https://geoportal.gov.mb.ca/search?collection=Dataset&q=crop%20yields)

### Step 2: Gather GIS Data

* Incorporate Geospatial data for each of RM's from provinces
* RM data was missing for the SK RM's 278, 408, and 529 and MB RM's UNORG TERRITORY, luckily these don't appear in our top 10 list so this missing data can be ignored for this analysis.
  * with these 4 missing RMs we end up losing 208+ (of 27k) rows of data trying to display them as geospatial data 
* 478 Total Rural Municipalities (RM) have shape files available for SK and MB (3 duplicates)
* Source: [Shapefiles provided](https://github.com/cboyda/AgTech/tree/main/Data)

### Step 3: Gather Canola Pricing

* Grab Canola stock prices
* 3285 daily Stock prices found for Canola as $ per Tonne and **$ per Bushel** (selected) (averaged for each year)
* Now our Yield and Value Data is limited to Years 2010-2022
* Stock Price Source: [investing.com](https://www.investing.com/commodities/canola-futures-streaming-chart)

### Step 4: Methodology: Partitional Clustering
Utilized unsupervised learning and clustering analysis.

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

## DETAILS
<details>
  <summary>ANALYSIS DETAILS... [click to view]</summary>
&nbsp;
&nbsp;
&nbsp;
  
  
#### K-Means
K-means is a partitioning-based clustering algorithm. It assigns data points to clusters by minimizing the sum of squared distances between data points and the centroid of their assigned cluster. It assumes that clusters are spherical and equally sized.

* k-mean elbow graph for selecting preferred k value
![elbow graph](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/elbow-Value_scaled.png)

* k-mean silhouette analysis graph which validated my k=2/4 choices
![silhouette graph](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/silhouette_kmeans_clusters.png)

![k-means results](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/k-means_comparison_data.png)

#### DBSCAN
DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is a density-based clustering algorithm. It defines clusters as dense regions of data points separated by areas of lower density. It doesn't assume spherical clusters and can discover clusters of arbitrary shapes.

![dbscan results](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/DBSCAN_results.png)

  * See Python code for more details, preference was to focus on results of k-means since they visually represented a clearer result

</details>

# Results
Provided in full detail as a Microsoft PowerPoint presentation, choose which you wish to view:
* [Slides as PDF](https://github.com/cboyda/AgTech/blob/main/Visuals/Capstone%20-%20High%20Value%20Canola.pdf)
* [Microsoft Powerpoint Slide in .PPT](https://github.com/cboyda/AgTech/raw/main/Visuals/Capstone%20-%20High%20Value%20Canola.pptx)
* [Complete Python notebook of analysis](https://github.com/cboyda/AgTech/blob/main/Assignments/CapstoneAssignment_CropAnalysis.ipynb)
  * Leveraged local workstation Anaconda with Python v3.12

### a) Exploratory Data Analysis (EDA)

![Yield vs Stock Prices](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/graph-Yield_vs_StockPrice.png)

![Correlation Matrix](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/correlation_matrix.png)

### b) Model Comparison
k-Means Clustering with k=2 and k=4.
![k=2 violinplot](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/cluster_k2_violin.png)
![k=4 violinplot](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/cluster_k4_violin.png)

### c) Insights
* Percentage Difference between Valuation and Crop Yield shows interesting patterns over time
![percentage histograms](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/graph-Diffs_Normalized_OverTime.png)

* Top 10 Canola RM locations.  Interestingly the Top 10 Canola RM's by YIELD are NOT the same as VALUE.  These interactive HTML files allow you to see the discrepancy. The reasons could be data discrepancy but it is an interesting insight and begs the question, why?
* Interactive Top 10 RM's [Yield HTML Map](https://raw.githack.com/cboyda/AgTech/main/Visuals/Canola_TopYields.html)

![Top10byYield](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/Top10Yields_data.png)
 
* Interactive Top 10 RM's [Values HTML Map](https://raw.githack.com/cboyda/AgTech/main/Visuals/Canola_TopValues.html)

![Top10byValue](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/Top10Values_data.png)

## Data Visualizations
* Interactive Python Widget
![Interactive Python](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/Interactive_Python.png)

* Interestingly only 3 RM's resulted a negative difference:
![Negative_RM_Differences](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/negative_RM_percent_difference.png)
* These 3 RM's invite further exploration, why are they negative, what is going on in these regions?
  * For RM 46 (SK), the Canola yield had a mean of 16.79 with a standard deviation of 11.77, while the Value had a mean of 224.02 with a standard deviation of 113.11. The Canola was scaled to 0.00, and the Value was scaled to 0.04. The diff_percent_yield_value is -100.00, indicating a decrease.
  * For RM REYNOLDS (MB), the Canola yield had a mean of 36.55 with a standard deviation of 11.19, while the Value had a mean of 629.82 with a standard deviation of 313.03. The Canola was scaled to 0.71, and the Value was scaled to 1.00. The diff_percent_yield_value is -29.20, indicating a decrease.
  * For RM STUARTBURN (MB), the Canola yield had a mean of 29.34 with a standard deviation of 13.38, while the Value had a mean of 490.84 with a standard deviation of 377.04. The Canola was scaled to 0.45, and the Value was scaled to 0.67. The diff_percent_yield_value is -32.80, indicating a decrease.


* Interactive All Yield Map in HTML
[Yield HTML Map](https://raw.githack.com/cboyda/AgTech/main/Visuals/Canola_AllYields.html)

![YieldMap](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/mass_Canola_Yield_standardized.png)

* Interactive All Values Map in HTML
[Values HTML Map](https://raw.githack.com/cboyda/AgTech/main/Visuals/Canola_AllValues.html)

![ValueMap](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/mass_Canola_Value_standardized.png)

## Challenges
* GIS shapefiles were missing for 4 RMs for the best visualization these should be included

## Future Goals
* Would love to explore, does higher yield always mean higher quality crop?
* Better accuracy: use province-specific pricing like [Manitoba Canola specific prices](https://geoportal.gov.mb.ca/datasets/manitoba::manitoba-crop-prices-historical/explore) instead of generalizing with stock prices for all locations
* Add Alberta Crop Yield Information and GIS shapefiles
* Consider exporting as database, SQLlite and using LLM [Vanna-github](https://github.com/vanna-ai/vanna) / [Vanna.ai](https://vanna.ai/) for natural language queries
