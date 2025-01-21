# UMD MSML/DATA-602 - Principles of Data Science Group Project

## Group Members

- [Ashish Kumar Singh - aksingh4@umd.edu ]()
- [Nigar Aliyeva - naliyeva@umd.edu ]()
- [Kunal Goel - kgoel@umd.edu ](kgoel@umd.edu)
- [Deepika Ghotra - dghotra@umd.edu ](dghotra@umd.edu)
- [Priya Gutti - gutti@umd.edu](pgutti@umd.edu)
- [Aneesh Hatkar - ah16@umd.edu ](ah16@umd.edu)


## Project Part 1: Description and Proposal

## Index

- [Project Part 1: Data Collection, Exploration and project outline](#dataset-description)
- [Project Part 2: Data Preprocessing and Feature Engineering](#project-part-2-data-preprocessing-and-feature-engineering)

Things we are planning on doing in the preprocessing/data cleaning steps:
- Weather ID column has any duplicates and verifying if it is a primary key
- Convert the date columns to proper parsable date format
- Convert all the numerical columns to proper numerical format (int/float)
- Subtract the end date from the start date to sanity check the data
- Check for outliers in the data 
- Data cleaning (eg, we can check if empty values aren't filled with 'None' or 'N/A' etc)
- Get the correlation matrix of the dataset (Make a encoding for the categorical columns)
- Figure out which columns to drop and what to keep
- Check for interesting paterns in the data (like the distribution etc)
- Do feature engineering (eg, Subtract time start to end to get the duration etc)

## Dataset Description

This is a dataset of US car accidents, published on Kaggle, from 2016-2023. Here is the brief description of the dataset:

```
This is a countrywide car accident dataset that covers 49 states of the USA. The accident data were collected from February 2016 to March 2023, using multiple APIs that provide streaming traffic incident (or event) data. These APIs broadcast traffic data captured by various entities, including the US and state departments of transportation, law enforcement agencies, traffic cameras, and traffic sensors within the road networks. The dataset currently contains approximately 7.7 million accident records. For more information about this dataset, please visit here.
``` 

We would be using a subset of this dataset for our project, mostly from 2022-2023 owing to the size of the dataset. 

Dataset Link: https://drive.google.com/drive/folders/10PUo_SwddCOuP29YthV6cE8qjJq1GTIm?usp=sharing

# Project Part 2: Data Preprocessing and Feature Engineering

## (1) Objective of the Project
We aim to predict the **severity** and **duration** of accidents based on various factors such as location, time, date, weather conditions, road conditions, visibility, and others.

### Planned Columns for Prediction:
- **Severity of the accident**
- **Duration of the accident** (if attainable)

### Planned Columns to Use for Prediction:

#### Traffic Attributes:
- **Datetime**
- **Day of week** [categorical] {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday}  
  (Derived from the date column)

#### Address Attributes:
- **Location**
- **City** [categorical]
- **State** [categorical]
- **Geography** [categorical] {Mountainous, Coastal, Desert, Plains, Other}  
  (Derived from geographical information)
- **Development** [categorical] {Urban, Suburban, Rural}  
  (Derived from geographical information)

#### Weather Attributes:
- **Season** [categorical] {Winter, Spring, Summer, Fall}  
  (Derived from the date column)
- **Weather Condition**
- **Temperature** [numerical]
- **Wind Speed** [numerical]
- **Precipitation** [numerical]
- **Road Conditions** [categorical] {Dry, Wet, Snow, Ice, Other}
- **Visibility**

#### Points of Interest (POI) Attributes:
- **Railway Crossing**
- **Junction**
- **Traffic Signal**
- **Roundabout**
- **Period of the day** [categorical]

## (2) Feature Engineering

We plan to perform the following feature engineering steps:

- Use the date and time columns to derive new columns such as time of day, day of the week, month, season, etc.
- Simplify the weather conditions column into broader categories (e.g., Rain, Snow, Ice, Other).
- Extract geographical information from location data (e.g., Mountainous, Coastal, Desert, Plains, Other).
- Create a column indicating the development level of a city based on location data (e.g., Urban, Suburban, Rural).
- Apply frequency encoding to temporal data (e.g., encode minute, street, and city name columns).
- Use Principal Component Analysis (PCA) to reduce dataset dimensionality by condensing numerous columns into a few principal components.

## (3) Data Imputation and Balancing

### Imbalanced Severity Distribution:
```plaintext
Severity
2 3227546
3 226042
4 81224
1 38026
```
### Decision on Handling Imbalance

The class imbalance between severity level 4 and the other categories is approximately **1:42**. To address this, our strategy includes the following steps:

- **Compensation Methods**: We will assign higher weights to the minority class (severity level 4) during model training without altering the data distribution. Following best practices, we will begin by using compensation techniques to balance the model’s performance.
  
- **Undersampling as Backup**: If compensation methods underperform, we may apply **undersampling** to the majority classes, taking into account the large dataset size.

- **Risk of Overfitting**: **Oversampling** the minority class could lead to overfitting, which we will carefully avoid.

- **Hybrid Sampling & SMOTE**: We will also explore a combination of **under- and oversampling** techniques, along with **SMOTE**, for comparative analysis to achieve optimal results.

This approach provides a balance between flexibility and efficiency, ensuring the model can handle class imbalance effectively while minimizing the risk of overfitting.


# Project Part 3: Data Analysis and Model Building

## All the main code and project report is at [Project Report](ProjectPart3.ipynb)

# Project Part 4: Data Visualizations

## The main notebook is at [Project Part 4](ProjectPart4.ipynb). However, due to the massive size of the file, we have uploaded the same to colab, and the link is [here](https://colab.research.google.com/drive/172HZmX7l9PuIUKtUe7LNR2xy7pEo4MND?usp=sharing).

## We have the following major visualizations in the notebook:

### 1. US Accidents Severity Heatmap (2021-2023)

- **Description:** A Folium heatmap displaying the geographical distribution of accidents across the US, with severity indicated by intensity.
- **Purpose:** Identify accident hotspots and spatial patterns in severity.

### 2. Distribution of Accident Severity Levels

- **Description:** A Plotly Express histogram showing the frequency of accidents by severity level (1 to 4).
- **Purpose:** Understand the prevalence of each severity level.

### 3. Top 10 Features Correlated with Accident Severity

- **Description:** A horizontal bar chart depicting the top 10 features most correlated with accident severity.
- **Purpose:** Highlight key factors associated with severity for further analysis.

### 4. Top 10 States with Highest Accident Counts

- **Description:** A bar chart listing the top 10 states by number of accidents.
- **Purpose:** Identify regions with the highest accident occurrences.

### 5. Frequency of Traffic Factors Associated with Incidents

- **Description:** A bar plot showing how often specific traffic factors (e.g., traffic signals, junctions) are present in accidents.
- **Purpose:** Assess the impact of environmental and infrastructural factors on accidents.

### 6. Distribution of Weather Factors

- **Description:** A boxplot illustrating the distribution of various weather parameters (Temperature, Humidity, etc.) sampled from the dataset.
- **Purpose:** Analyze weather conditions prevalent during accidents.

### 7. Distribution of Accidents by Hour (Weekends vs. Weekdays)

- **Description:** A line plot comparing accident percentages by hour for weekends and weekdays.
- **Purpose:** Reveal temporal patterns and peak hours for accidents.

### 8. Weekly Distribution of Road Accidents

- **Description:** A bar chart showing the percentage of accidents occurring each day of the week.
- **Purpose:** Identify days with higher accident rates.

### 9. Incidents Over Time (Monthly)

- **Description:** A line chart displaying the number of incidents per month from 2021 to 2023.
- **Purpose:** Observe trends and fluctuations in accident occurrences over time.

### 10. US Accidents Severity Map (2021-2023)

- **Description:** An interactive Folium map with clustered markers colored by accident severity.
- **Purpose:** Provide detailed geographical visualization of accidents.

### 11. Correlation Heatmap of Top Features Related to Accident Severity

- **Description:** A heatmap of correlation coefficients among top features related to severity.
- **Purpose:** Visualize relationships between key variables affecting severity.
