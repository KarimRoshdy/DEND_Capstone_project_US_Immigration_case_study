# Immigration Study Case
### Data Engineering Capstone Project

#### Project Summary
This project is aimed to create databases for immigration in USA and local tempeatures in USA. Starting from gathering data from multiple sources then applying some data cleaning and wrangling steps to make data more suitable for our purposes. At The end all data are stored in parquet files partitioned by suitable columns, which can be later easily retrieved and further processed or integrated. 

The project follows the follow steps:
* Step 1: Scope the Project and Gather Data
* Step 2: Explore and Assess the Data
* Step 3: Define the Data Model
* Step 4: Run ETL to Model the Data
* Step 5: Complete Project Write Up

### Step 1: Scope the Project and Gather Data

#### Scope 
In this project we will study the immigration to USA and answer two question at the end:
1. The top 5 nationalities immigrated to USA
2. The best 5 cities to immigrants in USA

Tools: Apache Spark 

#### Describe and Gather Data 
* I94 Immigration Data: This data comes from the US National Tourism and Trade Office  (https://travel.trade.gov/research/reports/i94/historical/2016.html).
* World Temperature Data: https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data

### Step 2: Explore and Assess the Data
#### Explore the Data 
we will filter data and remove duplicates for each dataset. In addidion missing data will be dropped
#### Cleaning Steps
* Dropping missing data and duplicates 
* Filteration of data based on the country and othe aspects of this study
* Casting new created or already defined columns with the right data types

### Step 3: Define the Data Model
#### Fact table: immigration with columns
* cicid 
* i94yr 
* i94mon
* i94res (origin_country)
* i94port
* arrdate 
* i94addr (destination)
* depdate
* i94mode (transportation)

#### Dimension tables: 
1. immigrant_table
* cicid
* i94bir
* count
* i94visa
* biryear
* gender

2. temperature
* year
* month
* avg_temp_celcius
* avg_temp_fahrenheit
* state_abbrev (i94port)
* City
* Country

### Step 4: Run Pipelines to Model the Data 
#### 4.1 Create the data model
We need a data model which enbales flexible queries to be run. I chose the relational model (SQL) to build a star schema to store our data. It is very common to use SQL since we might change our queries in the future. 
##### At the beginning we would like to know the most visited cities in USA and the top nationalities immigrating to USA.
* Query1: The top 5 nationalities immigrated to USA.
* Query2: The best 5 cities to immigrants in USA.



#### 4.2 Data Quality Checks
Explain the data quality checks you'll perform to ensure the pipeline ran as expected. These could include:
 * Integrity constraints on the relational database (e.g., unique key, data type, etc.)
 * Unit tests for the scripts to ensure they are doing the right thing
 * Source/Count checks to ensure completeness
 
 #### 4.3 Data dictionary 
 #### Fact table: immigration with columns
 * cicid >> a unique number for the immigrants.
 * i94yr >> 4 digit year
 * i94mon >> Numeric month
 * i94res >> is country from where one has travelled.
 * i94port >> 3 character code of destination USA city.
 * arrdate >> is date of arrrival.
 * i94addr >> is where the immigrants resides in USA.
 * depdate >> the Departure Date from the USA
 * i94mode >> 1 digit travel code (transportation)

 #### Dimension tables: 
 1. immigrant_table
 * cicid >> a unique number for the immigrants.
 * i94bir >> Age of respondent in years.
 * count >> no. of entry.
 * i94visa >> is the type of visa which one owns.
 * biryear >> 4 digit year of birth
 * gender >> gender

 2. temperature
 * year >> 4 digit year
 * month >> Numeric month
 * avg_temp_celcius >> temperature in °C
 * avg_temp_fahrenheit >>  temperature in °F
 * i94port >> 3 character code of destination USA city
 * City >> city name
 * Country >> country name

 #### Step 5: Complete Project Write Up
* Clearly state the rationale for the choice of tools and technologies for the project.
###### In this project I have mainly used:
1. Apache Spark: a very powerful data-handling tool, which enables processing big data from various data sources (e.g. SAS, CSV, JSON, XML ...etc.) in a convenient and easy way. In addition it enables distribution of data on mulitple CPUs and well-suited for expanding data on AWS with EMR clusters.
2. Jupyter Notebook: It has been applied in this project for buliding data pipelines because it has the power to display the data in a quick and beautiful way with less effort. It can also be used to integrate many libraries to serve our target (e.g. SQL, Spark, Pandas, Numpy .... etc.) 

* Propose how often the data should be updated and why.
Data should be monthly updated since the data is defined mothly in the big dataframe

* Write a description of how you would approach the problem differently under the following scenarios:
 * The data was increased by 100x.
###### It would be a good solution to still using spark but move it on AWS by creating EMR cluster.
 * The data populates a dashboard that must be updated on a daily basis by 7am every day.
###### We could use Airflow for this purpose with defined DAGs to be updated daily.
 * The database needed to be accessed by 100+ people.
###### Move the project to AWS and create user credentials for each user and defininig appropriate roles.

