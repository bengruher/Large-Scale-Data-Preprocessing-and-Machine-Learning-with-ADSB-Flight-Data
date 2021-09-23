# Flight-Data-Project

**Abstract:**

This project was completed as our Capstone project for our graduate Data Science program at Seattle University. The project involved taking 100's of GB's of ADS-B flight data (the data that is transmitted by all aircraft every few seconds) and transforming that data into actionable insights. The majority of the project was focused on processing the data. Once the data was processed, we used machine learning to try to predict runway wait times for commercial flights in the United States. Although our models did not perform well (most of our models were off by 20-30 minutes), we gained valuable experience in processing and managing large quantities of noisy data. 

**Data Source and Storage:**

We acquired our dataset from ADS-B exchange, which can be found at https://www.adsbexchange.com/. We initially ingested around 3 years worth of ADS-B data into an S3 bucket on AWS. This constituted 100's of GB's of raw JSON data. 

**Data Preprocessing:**

Due to the size of the data, JSON was not an efficient format to work with our data. We created an EMR cluster on AWS and using Spark, we converted all of the data into Apache Parquet format. Once the data was in Parquet, we were able to run efficient Spark jobs on the data to transform it into something more useful for our business problem. One of the main transformations we did was grouping the individual observations (transmission from a plane) into representations of entire flights. We were able to create features such as flight duration, departure airport, arrival airport, engine start time, average air speed, and many others.

We then processed the data a second time to generate features that were relavant to our specific task. For example, we created a runway wait time feature that served as the class label in our downstream machine learning task. 

All of these operations involved processing data at very high scale. 

**Machine Learning:**

Unfortunately, data collection and preprocessing took up the majority of our time for the project so we were only able to spend a few days on creating machine learning models to try to predict runway wait time. In an initial attempt at modeling, we used the Amazon Sagemaker built-in linear learner algorithm. We also trained an XGBoost on a local machine. Both models resulted in predictions that were on average 20-30 minutes different than the actual runway wait time. 
