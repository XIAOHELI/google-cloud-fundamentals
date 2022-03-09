###  Overview of IAM
- GCP has managed relational and NoSQL database services  
- Traditional web and line-of-business apps may use RDBMS  
- Modern applications rely on NoSQL databases  
- Web-scale, distributed applications need multi-region
 databases  
- In-memory database is used for accelerating the performance of apps  

### 1.Google Cloud SQL (SQL DB)
- Fully managed RDBMS(relational database management system) service that simplifies set up, maintain, manage, and administer database instances  
  + can setup a cluster of database servers that are going to be completely managed by google.

- Cloud SQL supports three types of RDBMS  
  + MySQL  
  + PostgreSQL  
  + Microsoft SQL Server (Preview)  

- A managed alternative to running RDBMS in VMs  

- Cloud SQL delivers scalability, availability, security, and reliability of database instances  

- Cloud SQL instances may be launched within VPC for additional security  
  + This will isolate your database instance from the rest of the deployments and makes it more secure so you may want to run this is a private subnet of a VPC while your front end is going to run in the public subnet with very limited access to the back end database resources.

### 2.Google Cloud Bigtable (NoSQL DB)
- Petabyte-scale, managed NoSQL database service  

- Sparsely populated table that can scale to billions of rows and thousands of columns  

- Storage engine for large-scale, low-latency applications  

- Ideal for throughput-intensive data processing and analytics  

- An alternative to running Apache HBase column-oriented database in VMs  

- Acts as a storage engine for MapReduce operations, stream processing, and machine-learning applications
  + GCP customers rely on cloud BigTable as an alternative to running and Apache HBase database in the cloud.  
  + it is becoming the preferred database for running big data and analytic workloads.  

### 3.Google Cloud Spanner (RDBMS & NoSQL)
- Managed, scalable, relational database service for regional and global application data   

- Scales horizontally across rows, regions, and continents -> make it different than other databases   
  + + so you can technically set up a cloud spanner database that runs in multiple regions that is technically multiple continents and your friend and application can be deployed in each of these regions that can talk to the instance which is a globally distributed database powered by cloud spanner.

- Brings best of relational and NoSQL databases
  + relational databases are also known to have highly transactional, and highly consistent, transaction support.   
  + nosql databases are known for their scale-out ability so you can very quickly add additional nodes to an existing nosql database cluster and gain higher availability and higher redundancy they also delivered more scale.  
  + **best thing about cloud spanner is the ability to get the best of relational and nosql databases, see below.

- Supports ACID transactions and ANSI SQL queries
  + deliver highly consistent transactions that are asset complained and also support an ANSI SQL queries while it can scale out pretty much like in nosqll database.

- Data is replicated synchronously with globally strong consistency   
  + if you are running two or more instances of cloud spanner across Asia Europe and America, as soon as you write in Asia, data becomes instantly available in Europe and America, thus, this is a truly globally distributed database with strong consistency.

- Cloud Spanner instances run in one of the three region types:   
  - Read-write region
    + where you perform typical transactions and commit them.    
  - Read-only region   
    + where you read the data that is written in one of the other regions and this will increase the throughput because you don't have the burden of writing and replicating synchronizing and locking the data.  
  - Witness region
    + essentially responsible for making sure that the data is synchronized and replicated in the most consistent form so it keeps an eye on the other instances to ensures that the application is always reading from the most consistent and most healthy instance of the cloud spanner database instance.  

### 4.Google Cloud Memorystore
- A fully-managed in-memory data store service for Redis   

- Ideal for application caches that provides sub- millisecond data access  
  + Cloud memory store typically sits in between your front-end　application, that is querying data from the data store very often and, every time you fetch the data it gets cached with in-memory store so subsequent retrieve operations or fetch operations won't go all the way to the database but instead, they get picked up from the in-memory cache maintained by memory store that's how it accelerates the performance by reducing the latency of data retrieval.  

- Cloud Memorystore can support instances up to 300 GB and network throughput of 12 Gbps  
  + help you cache frequently access data sets even the large data sets and avoid the round-trip to the database.  

- Fully compatible with Redis protocol  

- Promises 99.9% availability with automatic failover  

- Integrated with Stackdriver for monitoring  

### 5.Demo - Provisioning Google Cloud SQL Instance
```


```
