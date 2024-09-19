# UMD MSML/DATA-602 - Principles of Data Science Group Project

## Group Members

- [Ashish Kumar Singh - aksingh4@umd.edu ]()
- [Nigar Aliyeva - naliyeva@umd.edu ]()
- [Kunal Goel - kgoel@umd.edu ](kgoel@umd.edu)
- [Deepika Ghotra - dghotra@umd.edu ](dghotra@umd.edu)
- [Priya Gutti - gutti@umd.edu](pgutti@umd.edu)
- [Aneesh ]()


## Project Description and Proposal

## Index

- [Project Part 1: Data Collection, Exploration and project outline](./Data%20Exploration.ipynb)

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
```This is a countrywide car accident dataset that covers 49 states of the USA. The accident data were collected from February 2016 to March 2023, using multiple APIs that provide streaming traffic incident (or event) data. These APIs broadcast traffic data captured by various entities, including the US and state departments of transportation, law enforcement agencies, traffic cameras, and traffic sensors within the road networks. The dataset currently contains approximately 7.7 million accident records. For more information about this dataset, please visit here.
``` 

We would be using a subset of this dataset for our project, mostly from 2022-2023 owing to the size of the dataset. 

Dataset Link: https://drive.google.com/drive/folders/10PUo_SwddCOuP29YthV6cE8qjJq1GTIm?usp=sharing