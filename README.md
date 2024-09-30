# UMD MSML/DATA-602 - Principles of Data Science Group Project

## Group Members

- [Ashish Kumar Singh - aksingh4@umd.edu ]()
- [Nigar Aliyeva - naliyeva@umd.edu ]()
- [Kunal Goel - kgoel@umd.edu ](kgoel@umd.edu)
- [Deepika Ghotra - dghotra@umd.edu ](dghotra@umd.edu)
- [Priya Gutti - gutti@umd.edu](pgutti@umd.edu)
- [Aneesh ]()


## Project Part 1: Description and Proposal

## Index

- [Project Part 1: Data Collection, Exploration and project outline](#dataset-description)
- [Project Part 2: Data Preprocessing and Feature Engineering](#project-part-2-data-preprocessing-and-feature-engineering)

Things we are planning on doing in the preprocessing/data cleaning steps:
- Wether ID column has any duplicates and verifying if it is a primary key
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

## Project Part 2: Data Preprocessing and Feature Engineering

### (1) Objective of the project

We are planning to predict the likelihood and severity of an accident based in a certain area based on the time, date, weather conditions, road conditions, visibility, and other factors. We also plan on trying to predict the duration of the accident based on the same factors (if possible).

** Columns to predict: **
- Severity of the accident
- Duration of the accident (if possible)

** Columns to use for prediction (including feature engineered ones): **
- Temporal Data
    - Time of day [categorical] {Morning, Afternoon, Evening, Night} (Derived from the time column)
    - Day of week [categorical] {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday} (Derived from the date column)
    - Month [categorical] {January, February, March, April, May, June, July, August, September, October, November, December} (Derived from the date column)
    - Season [categorical] {Winter, Spring, Summer, Fall} (Derived from the date column)
- Weather Conditions
    - Temperature [numerical]
    - Wind speed [numerical]
    - Precipitation [numerical]
    - Road conditions [categorical] {Dry, Wet, Snow, Ice, Other}
    - Visibility
- Location
    - City [categorical]
    - State [categorical]
    - Geography [categorical] {Mountainous, Coastal, Desert, Plains, Other} {Derived from global information}
    - Development [categorical] {Urban, Suburban, Rural} {Derived from global information}
- POI (Point of Interest) [categorical] {Railway crossing, Junction, Traffic signal, Roundabout}

### (2) Feature Engineering

We plan on doing the following feature engineering steps:
- Use the date and time columns to derive new columns like time of day, day of week, month, season etc
- Use the geo location to derive new columns like city, state, country etc
- Use PCA (Principal Component Analysis) to reduce the dimensionality of the dataset (Condense the numerous columns into a few principal components)
- Simplify the weather conditions column into a few categories (eg, Rain, Snow, Ice, Other)
- Derive Geo information from the location data (eg, Mountainous, Coastal, Desert, Plains, Other)
- Derive Development information from the location data (eg, Urban, Suburban, Rural)
- Use Frequency Encoding for temporal data (eg, Encode minutes of duration into a frequency encoding, street and city names etc)

### (3) Data Imputation and balancing

Decision on Handling Imbalance:

If the class imbalance is severe (e.g., minority class represents less than 10% of the data):

We will use SMOTE (Synthetic Minority Over-sampling Technique) to create synthetic examples of the minority class, as well as random undersampling of the majority class.
Our approach will be: "Create synthetic data for the minority class(es) using SMOTE to achieve a more balanced distribution, aiming for at least a 3:7 ratio between minority and majority classes, maybe also use random undersampling to further balance the classes."

**We would be balancing the Severity column as the class distribution is highly imbalanced:**
```
Severity
2    3227546
3     226042
4      81224
1      38026
```

If the class imbalance is moderate (e.g., minority class represents 10-30% of the data):

We will use a combination of oversampling the minority class and undersampling the majority class.
Our approach will be: "Apply a combination of random oversampling to the minority class and random undersampling to the majority class to achieve a 4:6 ratio between classes."


If the class imbalance is mild (e.g., minority class represents 30-40% of the data):

We will primarily rely on algorithmic approaches rather than data-level techniques.
Our approach will be: "Adjust class weights in the model to give more importance to the minority class during training. We will not alter the data distribution itself."


If the classes are relatively balanced (e.g., no class represents less than 40% of the data):

We will not use any specific techniques to deal with imbalanced data.
Our justification will be: "All classes are at worst imbalanced 4:6, which is not severe enough to require special handling techniques. Standard machine learning algorithms should perform adequately without additional balancing."
