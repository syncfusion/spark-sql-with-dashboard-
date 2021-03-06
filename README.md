##Summarize a billion records using the Syncfusion Dashboard Platform###
###Prerequisite 

Download and install Syncfusion Big Data Platform and Dashboard Platform from below links

[Big Data Platform](https://www.syncfusion.com/products/big-data)

[Dashboard Platform](https://www.syncfusion.com/products/dashboard)

###Upload the data set into HDFS
Perform below steps to upload the data set into HDFS.

1. Download the dataset from the following link [DataSet] (https://data.cityofnewyork.us/data?agency=Taxi+and+Limousine+Commission+%28TLC%29&cat=&type=new_view&browseSearch=&scope) 

2. Open the command prompt and locate %HADOOP_HOME%\bin 
3. Execute the  below command 

	```hdfs dfs -put <localfolderpath> /SparkSQLDemo/```

###Syncfusion Bigdata ThriftApplication
Follow below syntax to run the sample queries using Syncfusion Bigdata ThriftApplication

#####Syntax
	Syncfusion.Bigdata.ThriftApplication.exe “Spark-Thrift Server hostname: Port” “Query”

####Create and load the data into the Table 
To create table nyctrips and load the data from HDFS, We need to execute below query

#####Query
	CREATE EXTERNAL table nyctrips(vendor_id string,pickup_datetime timestamp,dropoff_datetime timestamp,passenger_count double,trip_distance  double,pickup_longitude double,pickup_latitude double,rate_code double,store_and_fwd_flag string,dropoff_longitude double,dropoff_latitude double,payment_type  string,fare_amount double,surcharge double,mta_tax double,tip_amount double,tolls_amount double,total_amount double) ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
	LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2009.csv' INTO TABLE nyctrips
	LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2010.csv' INTO TABLE nyctrips
	LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2011.csv' INTO TABLE nyctrips
	LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2012.csv' INTO TABLE nyctrips
	LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2013.csv' INTO TABLE nyctrips
	LOAD DATA INPATH '/SparkSQLDemo/nyc_taxi_data.csv' INTO TABLE nyctrips
	LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2015-01-06.csv' INTO TABLE nyctrips
  
  
Execute the commands given below to create and load the data into the table nyctrips using ThriftApplication 

#####Commands
Command to create table **nyctrips**

	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "CREATE EXTERNAL table nyctrips(vendor_id string,pickup_datetime timestamp,dropoff_datetime timestamp,passenger_count double,trip_distance  double,pickup_longitude double,pickup_latitude double,rate_code double,store_and_fwd_flag string,dropoff_longitude double,dropoff_latitude double,payment_type  string,fare_amount double,surcharge double,mta_tax double,tip_amount double,tolls_amount double,total_amount double) ROW FORMAT DELIMITED FIELDS TERMINATED BY ','"
	
Command to load the data to table

	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2009.csv' INTO TABLE nyctrips"
	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2010.csv' INTO TABLE nyctrips"
	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2011.csv' INTO TABLE nyctrips"
	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2012.csv' INTO TABLE nyctrips"
	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2013.csv' INTO TABLE nyctrips"
	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/nyc_taxi_data.csv' INTO TABLE nyctrips"
	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "LOAD DATA INPATH '/SparkSQLDemo/yellow_tripdata_2015-01-06.csv' INTO TABLE nyctrips""
	
####Caching the table 
Execute below command to cache the table nyctrips.

	Syncfusion.Bigdata.ThriftApplication.exe spark-thriftserverhostname:port "cache table nyctrips"

####Partitioning the table based on year 
By using SQL context, we are partitioning the table **nyctrips** by year in spark-shell

1. Open the SPARK-SHELL by using the command

	%SAPRK_HOME%\bin > spark-shell --master yarn-client
		
2. After starting the spark-shell pass the command as below
	
  1. Load the nyctrips table data into the Data Frame

	```scala > var nycTripsData = sqlContext.sql("select * from nyctrips")```
	
	```scala > var partitionByYear = nycTripsData.repartition(year($"dropoff_datetime"))```
	
  2. Save the partitioned result into the new Table "nyctrips_partitionbyyear"
	
	```scala > partitionByYear.saveAsTable("nyctrips_partitionbyyear")```

###License
Copyright 2016 Syncfusion Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

 http://www.apache.org/licenses/LICENSE-2.0
    
Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
