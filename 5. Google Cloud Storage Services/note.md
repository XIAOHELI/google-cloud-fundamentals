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

-  Data can be stored within a single region, dual-region, or multi-region. [more details](https://cloud.google.com/docs/geography-and-regions#regional_resources)  
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
  + Best for disaster recovery and data accessed less than **once a quarter**.   
  + e.g. insurance policy file...  

- Archive
  + Best for long-term digital preservation of data accessed less than **once a year**.  

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
    + if you have a scenario where you need to attach the disk to one VM for read-write access but read the data from multiple VMs, in a read-only mode you can do that with persistent disks, so one VM will act as the writer, and all other VMs will act as readers. In this way,  you can designate one VM for read/write while adding multiple VMs that are quickly reading from the same disk with read-only access.   
    This opens up a lot of opportunities where you need to create distributed applications with centralized data access.   

-  Supports both SSD and HDD storage options    

-  SSD offers best throughput for I/O intensive applications  
    + like relational databases no sequel databases and so on.  
    + if you are running MongoDB inside a GCE VM or my sequel inside a GCE VM you might want to consider SSD.  

-  PD is available in three storage types:
    +  Zonal: you can launch the persistent disk that is confined to a specific zone.   
    +  Regional: provide higher availability and redundancy because data is constantly replicated within the same region or within the same location.    
    +  Local: same as above.  

### 3. Google Cloud Filestore
-  Managed file storage service for applications

-  **Delivers NAS-like filesystem** interface and a shared filesystem

-  Centralized, highly-available filesystem for GCE and GKE

-  Exposed as a NFS fileshare with fixed export settings and default Unix permissions

-  Filestore file shares are available as mount points in GCE VMs

-  On-prem applications using NAS take advantage of Filestore

-  Filestore has built-in zonal storage redundancy for data availability
    + means when you're writing data it is immediately replicated across multiple endpoints so that you have storage redundancy and this ensures higher availability of data.  

-  Data is always encrypted while in transit
```
summarize
Google Cloud file store emulates nas like environment in cloud, enabling legacy applications to continue to run while moving from on-prem to the cloud.

```

### 4.Demo of GCS
```
# Dashboard page, go to cloud storage

# buckets are going to be the containers within which we are going to create folders and store objects.

# we start by create the bucket and this is the highest level container within the GCS hierarchy so a bucket may contain a folder and a folder may contain a file.

# give a unique name

# click on continue

# choose where to store the data and continue

# next option is to apply permissions you can choose object level or bucket level permissions

# create with no size

# create a folder in the bucket

# we can upload file from local

```

5. Use Cases for GCP Storage Services (see the PDF)
- **Google Cloud Storage** -> Object Storage -> Scalable, durable and long-term storage -> centralized storage for frequently and infrequently accessed files.  

- **Persistent Disks** -> Block storage -> Attached to GCE VMs -> Dedicated attached storage for apps running in VMs based on HDDs and SSDs  

- **Cloud Filestore** -> File system -> NFS fileshare for GCE VMs -> NAS-like shared file storage with standard UNIX permissions
