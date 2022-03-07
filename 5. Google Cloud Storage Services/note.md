###  Overview of GCP Storage Services
-  Why do we need GCP storage services? -> Storage services add persistence and durability to applications.
-  Storage services are classified into three types:
    + Object storage  
    + Block storage  
    + File system  
-  GCP storage services can be used to store:
    +  Unstructured data(e.g. Images,PDF,HTML files,etc)  
    +  Folders and Files(typically migrating from your local on-prem data center)    


### 1.Google Cloud Storage
-  Unified object storage for a variety of applications  

-  Applications can store and retrieve objects through single API

-  GCS can scale to exabytes of data  

-  GCS is designed for 99.999999999% durability  
   + the change of losing data is almost 0%.  

-  GCS can be used to store high-frequency and low-frequency access of data  
    + storage service that can be used by cloud applications so when you are storing data you write the data using the API s-- and you also retrieve it using the api this is the fundamental difference between dealing with filesystem and an object storage.  

-  Data can be stored within a single region, dual-region, or multi-region[more details](https://cloud.google.com/docs/geography-and-regions#regional_resources)  
    + **regional(single region)**:Regional resources are resources that are redundantly deployed across multiple zones within a region, for example App Engine applications, or regional managed instance groups. This gives them higher availability relative to zonal resources.  
    + **dual-region**: Your Data is replicated across a specific pair of zones. Good for when you need colocated compute and storage and automatic failover.  
    + **multi-region**:Multiple Google Cloud services are managed by Google to be redundant and distributed within and across regions. These services optimize availability, performance, and resource efficiency. As a result, these services require a trade-off between either latency or the consistency model. These trade-offs are documented on a product specific basis.  

#### 1.1.Concept of Storage Classes
- Standard storage class(High Frequency Access)
  + the most common storage class used by developers.    
  + optimized for **low latency and frequent access** (e.g.if you are storing images that you are going to retrieve very often).

- Nearline storage class(Low Frequency Access)
  + meant for data access less frequently.  
  + typically chosen for data that is access less than once a month.  
  + lower cost than standard.

- Coldline  
  + Meant for data accessed least frequently.  
  + Chosen for data accessed less than **once in a year**.   
  + e.g. insurance policy file...  

```
suggestions:
Use Standard storage for High-performance object storage

Use Nearline or Clodline for Backup & archival storage
```

### 2.Persistent Disks
-  PD provides reliable block storage for GCE VMs
    + direct attached storage of your on-premises data center or the way you use USB storage. so persistent disks are essentially the block storage devices that can be attached to the Google compute engine instances or VMs.  

-  Disks are independent of Compute Engine VMs
    + you can create them outside of the context of a VM and retain it even after the VM is terminated.  
    + means more durable and reliable.

-  Each disk can be up to 64TB in size   

-  PDs can have one writer and multiple readers  

-  Supports both SSD and HDD storage options    

-  SSD offers best throughput for I/O intensive applications  
    
-  PD is available in three storage types:
    +  Zonal  
    +  Regional  
    +  Local   
