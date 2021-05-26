# FIS Offers - A Recommendation Engine

###### Team: `Sushma Padubidri,  Randy Geszvain, Bret Harvestine, Katie Smith`


## Bringing the FIS Merchant (Vantiv/WorldPay ) and FIS Issuing together with advanced data analytics

#### High Level Design
![Design Image](code/Arch.PNG)

-  Opportunity to promote FIS merchant's on the FIS issuer/ FI's.
-  Market penetration for FIS Merchant in areas with strong issuer influence.
-  Ability for FI's to provide customized and personalized offers to their customers.

## Solution Features

-  Data Merging 
-  Data Cleansing
-  Predictive analytics
-  Recommendations 
-  Visualization
-  API

## Data pipeline and framework

S3 -> Snowpipe -> Snowflake Table -> Kedro Data Engineering/Data Science Pipeline -> dashboard and API

### Technologies and Architecture  

- Snowflake and Hadoop
  - SQL
- Python
- Power BI
- Heroku API

### Open-source Software Used

-  Kedro
-  Pandas
-  Pandas_profiling
-  Pycaret
-  fuzzywuzzy
-  sklearn
-  numpy
-  scipy
-  Flask

## S3

S3 bucket allows users to upload new records and prepare for loading.

## Snowpipe

Snowpipe provides the ability to autoload data from s3 to a Snowflake table

##### Refer to bitbucket for creating Snowpipe SQL

## Snowflake Tables

Two Snowflake tables house issuer and merchant datasets.

:::info
Header Columns:
MER_NM,MER_ZIP,MONTH,MERCHANT_CATEGORY_XCD,CNT,SUM,SOURCE
:::

## Kedro Data Engineering/Data Science Pipeline

Kedro is an open-source Python framework for creating reproducible, maintainable, and modular data science code. The pipeline consists of nodes. Below shows the structure of our Kedro project.

- conf
    - base
        - catalog.yml
        - logging.yml
        - parameters.yml
    - local
        - credentials.yml
- data
    - raw
    - intermediate
    - primary
    - feature
    - model_input
    - models
    - model_output
    - reporting
- docs
- logs
- notebooks
- src
    - fis_inn
        - pipelines
            - data_processing
                - nodes(.py)
                - pipeline(.py)
            - data_science
                - nodes(.py)
                - pipeline(.py)

### Data Processing pipeline

The pipeline is consisted of several nodes and functions to preprocess data and prepare for data science projects.

#### Preprocess Data

Data preprocessing steps include:
- Data cleaning
    - remove rows contain a null value
- Remove Outliers
    - label encoder
    - calculate z score
    - remove records with z score > 3
- map/combine datasets
    - combine issuer and merchant data with the population using zipcodes
- Fuzzy matching
    - Merchant name standardization between two source datasets


#### Data Science

The Data science pipeline includes machine learning processing.
- Data profiling
    - data profiling provides initial visualization and overview of the preprocessed data
        - descriptive statistics
        - variables
        - correlations
        - missing values
- Cluster data
    - Clustered data divides the population or data points into a number of groups such that data points in the same groups are more similar to other data points
- Anomaly data
    - In data analysis, anomaly detection is the identification of rare items, events or observations which raise suspicions by differing significantly from the majority of the data
- Prophet prediction
    - an open-source prediction package that provides high accuracy of predicted data
- Linear Regression
    - split data
    - train model
    - evaluate model
    - save a pickle file for the model trained


#### Kedro Pipeline Diagram

This graph presents the Kedro pipeline that incorporates nodes, input, output files.

![Kedro Pipeline](code/kedro-pipeline.png)

## Dashboard

## API

An API built with flask can be deployed to Heroku or other provider platforms. Once we ran the machine learning algorithm in the data science pipeline, a pickle file can be generated and stored for retrieval. The pickle file stored the model. API can be utilized and called with certain parameters to get the prediction result.

## Cool and Wow factor

1. Cutting-edge and scalable technologies used.
2. User friendly from uploading the data to the report retrieval.
3. The pipeline is modular and re-producable.
4. Amazing and interactive dashboards to understand data.

## Takeaway(s) and Future Enhancements
