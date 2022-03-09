### Overview of Google Cloud Data and Analytics Services
- Data analytics include ingestion, collection, processing, analyzing, visualizing data  
  + each of those form a phase in the data processing pipeline.  

- GCP has a comprehensive set of analytics services  

- Cloud Pub/Sub is used for ingesting data at scale
  + whether it is telemetry data coming from sensors or logs coming from your applications and infrastructure, pub/sub could be the conduit to Google Cloud.

- Cloud Dataflow can process data in real-time or batch mode
  + The inbound data coming via pub/sub can be processed in real-time with data flow, it can also process historical data stored in Google Cloud Storage buckets or other sources in batch mode.

- Cloud Dataproc is a Big Data service for running Hadoop and Spark jobs  

- BigQuery is the data warehouse in the cloud  
  + customers rely on bigquery for analyzing historical data and deriving insights from that.  

- Cloud Datalab is used for analyzing and visualizing data  

### 1.Google Cloud Pub/Sub
- Managed service to ingest data at scale

- It based on the publishing/subscription pattern
  + where you have a set of publishers that send messages to a topic and you have subscribers that subscribe to the topic.

- Pub/Sub act as Global entry point to GCP-based analytics services
  + a channel whether you are ingesting telemetry data logs or any other data that is ingested into the cloud, it is typically sent via cloud pub/sub.  

- Acts as a simple and reliable staging location for data
  + but it is not meant to be a durable data store, just can be used for staging data as it enters the cloud and is waiting to get processed by cloud data flow or data proc. So it can deliver data to a variety of destinations depending on how the subscribers are configured.  

- Tightly integrated with services such as Cloud Storage and Cloud Dataflow
  + where you can use pub/sub to store inbound data for real-time processing through data flow.  

- Supports at-least-once delivery with synchronous, cross-zone message replication

- Comes with end-to-end encryption, IAM, and audit logging

### 2.Google Cloud Dataflow
- Managed service for transforming and enhancing data in real-time stream or data stored in cloud storage which is processed in batch mode  

- Based on Apache Beam open source project  

- Serverless approach automates provisioning and management  
  + you don't need to provision resources and scale them manually, instead you start streaming the data and connecting that to data flow via pub/sub and it can automatically start processing the data and scales the infrastructure based on the inbound data stream.  

- Inbound data can be queried, processed, and extracted for target environment  
  + data flow is typically used for manipulating data or pre-processing data as it comes into the cloud. The input for data flow could be Google cloud pub/sub, while the output of data flow could be written directly to bigquery or Google Cloud Storage or to one of the manager database services like cloud SQL.

- Tightly integrated with Cloud Pub/Sub, BigQuery, and Cloud Machine Learning  

- Cloud Dataflow connector for Kafka makes it easy to integrate Apache Kafka  
  + if you already have Kafka infrastructure with the connector it is possible for you to bridge Kafka with cloud dataflow and get best of the both worlds.  

### 3.Google Cloud Dataproc
- Managed Apache Hadoop and Apache Spark cluster environments  

- Automated cluster management  

- Clusters can be quickly created and resized from three to hundreds of node  

- Move existing Big Data projects to GCP without redevelopment  
  + because most of your existing map-reduce jobs that are targeting Hadoop or spark can run seamlessly on cloud data proc.

- Frequent updates to Spark, Hadoop, Pig, and Hive  
  + to maintain the platform with the latest updates so this makes cloud data proc very current and also it matches options available.  

- Integrates with other GCP services like Cloud Dataflow and BigQuery  
  + so in the data processing pipeline, data enters through pub/sub gets transformed through dataflow, and gets processed with data proc typically in the form of a map reduced job for apache Hadoop or apache spark, and the output of data proc can be stored in bigquery, or it can go to google cloud storage.  

### 4. Google Cloud Datalab
- Interactive tool for data exploration, analysis, visualization, and machine learning  

- Runs on Compute Engine and may connect to multiple cloud services  

- Built on open source Jupyter Notebooks platform  
  + an industry standard for analyzing and visualizing data sets.  

- Enables analysis data on BigQuery, Cloud ML Engine, and Cloud Storage    

- Supports Python, SQL, and JavaScript languages  
  + even though it runs on compute engine you don't need to provision a VM beforehand as a part of Google Cloud Data lab experience Google will provision a GCE VM that runs a Jupyter notebook environment.

### 5. Google BigQuery
- Serverless, scalable cloud data warehouse  
  + you can ingest data into bigquery and it automatically scales to support petabytes of data sets.

- Has an in-memory BI Engine and machine learning built in   
  + so as you query data from bigquery you can apply machine learning algorithms that can perform predictive analytics right out of the box.

- Supports standard ANSI:2011 SQL dialect for querying  
  + means you don't need to learn new languages or domain-specific languages to deal with bigquery. You can use familiar sql queries that support inner joins, outer joins, group by clauses, and where clauses to extract data and to analyze from existing data stores.

- Federated queries can process external data sources   
  + Cloud Storage  
  + Cloud Bigtable  
  + Spreadsheets (Google Drive)  

- Automatically replicates data to keep a seven-day history of changes   
  + means you can go back in time and look at some of the other queries and changes that were made to the original data set.  

- Supports data integration tools like Informatica and Talend  

### 6.Demo - Analyzing Data with BigQuery
```
we are going to analyze a data set provided by Stack Overflow to analyze the data. so we'll use bigquery to load the data set coming from Stack Overflow and perform certain queries.

----- BigQuery -----
# search BigQuery
# ADD DATA and Explorer public datasets and search stack overflow
# view dataset, it will open an new window for us to run queries

# run queries
SELECT badge_name AS First_Gold_Badge,
       COUNT(1) AS Num_Users,
       ROUND(AVG(tenure_in_days)) AS Avg_Num_Days
FROM
( SELECT
badges.user_id AS user_id,
badges.name AS badge_name,
TIMESTAMP_DIFF(badges.date, users.creation_date, DAY) AS tenure_in_days, ROW_NUMBER() OVER (PARTITION BY badges.user_id
                       ORDER BY badges.date) AS row_number
  FROM
    `bigquery-public-data.stackoverflow.badges` badges
  JOIN
    `bigquery-public-data.stackoverflow.users` users
  ON badges.user_id = users.id
  WHERE badges.class = 1
)
WHERE row_number = 1
GROUP BY First_Gold_Badge
ORDER BY Num_Users DESC
LIMIT 10

this query above is the number of gold badges that were assigned to users. so Stack Overflow has a ranking system and a voting system where if you answered multiple questions in a span of time and they get upvoted, you automatically get gold badges so this query will help us understand how many users got those badges and how long it took them and how many questions they really answered.

4.2 sec elapsed, 1.7 GB processed
From the Result, we can see it basically processed 1.2 GB of data in just 5.2 seconds and we are able to see this result so this is business intelligence data warehouse as a service where you can query gigabytes and petabytes of data in a matter of seconds and minutes.
```

### 7.GCP Data & Analytics Service -use cases
Google Cloud Pub/Sub -> Ingestion -> High-speed ingestion of data -> Sensor data, telemetry, and logs  

Google Cloud Dataflow -> Stream and batch processing -> Process data coming from Pub/Sub and data in GCS -> ETL for business intelligence and machine learning   

Google Cloud Dataproc -> MapReduce jobs -> Big Data processing -> based on Apache Hadoop and Spark -> MapReduce jobs   

Google Cloud Datalab -> Visualization -> Jupyter Notebooks for interactive analysis -> Data exploration and visualization   

BigQuery -> Data warehouse -> Query large datasets in ANSI SQL -> Business intelligence   
