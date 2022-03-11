### Overview of Additional Google Cloud Services including Anthos
# 1.Google Cloud IoT
- Cloud IoT Core  
  + provides machine-to-machine communication  
  + device registry   
  + overall device management capabilities  
  + provides authentication and authorization of devices  
  + tightly integrated with cloud pub/sub and cloud functions
    = so the telemetry the sensor data that is sent to cloud IOT core goes by a pub/sub and you can take it to cloud functions and perform serverless rules and serverless execution of business logic based on the inbound telemetry.

> if you have multiple sensors or multiple devices that need to be connected to the cloud, you can use IOT core. IOT core provides authentication and authorization of devices which enables machines to talk to each other and finally you can manage the entire lifecycle of devices.

- Edge TPU  
  + It is a hardware that is available to accelerate AI models running at edge
  > so if you are building a model using Google AI platform and you want to run it offline at the edge. so edge is essentially a device that can run business logic and even artificial intelligence models in offline mode. so when you are executing those models since they are not running on full-fledged hardware or full-fledged servers powered by GPUs, you still need to have additional hardware that can assist the CPU in speeding up inference and speeding up running the machine learning models. Therefore, edge TPU plays the role of a micro TPU or GPU that is attached to the edge devices. so when you run a TensorFlow model on a device powered by edge TPU, the inference is the process of performing classification, detection, or predictions will be much faster. Thereby edge TPU is available as a chip that is going to be attached to an edge device like a Raspberry Pi or an x86 device.

### 2.Google Cloud API Management
- Apigee API Platform
  + provides the capabilities for designing, securing, publishing, analyzing and monitoring API.  

- API Analytics
  + provide end-to-end visibility across api programs with developer engagement and business metrics
  = organizations using api analytics as a part of apigee tool or apigee platform can gain insights into api performance, usage metrics like traffic trends, spikes, latency response times and other custom criteria.
  = also help them make informed business decisions because they precisely know how their api's are being used by developers and their partners.

- Cloud Endpoints
  + meant to develop deploy and manage api's in the Google cloud environment   
  + it is based on an engine exposed proxy, and it uses open API specification as the API framework
  + help developers to manage the entire API development from the beginning till deploying and maintaining them
  + with tight integration with stackdriver, they can perform monitoring tracing and logging of api's

### 3.Google Cloud Hybrid & Multi-Cloud Services
- Traffic Director
  + route the traffic across virtual machines and containers deployed across multiple regions

- Stackdriver
  + A observability platform for tracing, debugging, logging and gaining insights into application performance and infrastructure monitoring

- GKE On-Prem
  + takes google kubernetes run engine and runs that within the local data center environment or on-premises

### 4.Anthos
**Why Google has invested in its service like Anthos?**  
> And for that, we need to have a decent understanding of Kubernetes.  

**What is Kubernetes?**  
> Kubernetes is a distributed computing platform. Like any other distributed computing platform, it has a master which is responsible for managing a set of worker nodes, and these worker nodes run the actual application or the workload.  

> That is the responsibility of the master when you deploy an application and you request the master to schedule the application in order to basically run it in one or more nodes.     
> It will take the request from you and then figure out which of the nodes are ready and capable of running your application.   
> In the end, it automatically schedules your application in one of these notes at a very high level.  

> One or more masters will have more worker nodes, and that's where the application is going to be deployed.   
> Moreover, the communities master is also called the control plane because it is ultimately responsible for orchestrating the infrastructure that is a set of cabinets and also orchestrating your application.  

In big Scale, we need Meta Control Plane(master) to manage maters that runs on different resources such as GCP, AWS or Azure. (e.g.Page 12)

What is Anthos?
