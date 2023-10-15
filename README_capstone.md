# Project: AgTech Capstone
Final Project | Cohort 4 | Stream 3

## Introduction
Reviewing crop prices, I was intrigued to see the Canola drastically increasing:
![Canola Pricing](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/CanolaPrices.png)
I was curious, if a rural municipal district has a high yield, how would that compare to its value? 
I assumed the top crop yield RMs would also have the highest valuation.

## Project Goals
This sample challenge is to go shopping for the best canola-valued fields.  Value will be calculated by taking the crop yield x stock crop price.
![Canola Valuation Function](https://raw.githubusercontent.com/cboyda/AgTech/main/Visuals/canola_function.png)

## Data Process
### Step 1: Crop Data

* Incorporate RM yields for numerous crops from both Saskatchewan and Manitoba
* Crop yields included for crop_columns=['Canola', 'Barley', 'Canary Seed', 'Durum Wheat', 'Lentils', 'Oats', 'Spring Wheat', 'Peas']

### Step 2: Gather GIS Data

* Incorporate Geospatial data for each of RM's from provinces
* RM data was missing for the SK RM's 278, 408, and 529 and MB RM's UNORG TERRITORY, luckily these don't appear in our top 10 list so this missing data can be ignored for this analysis.

### Step 3: Gather Canola Pricing

* Grab Canola stock prices
* Data was limited to 2010-2022

### Step 4: K-Means Clustering
<details>
  <summary>STATISTICAL MODEL DETAILS... [click to view]</summary>
  
#### Regression Statistical Models

#### Classification Statistical Models

</details>

# Results
### a) Model Comparison

### b) Quality of APIs

### c) Exploratory Data Analysis (EDA)

### d) Insights

### Step 5: Build Data Visualizations

## Challenges

## Future Goals
