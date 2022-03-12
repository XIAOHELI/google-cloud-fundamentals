### Overview of Additional Google Cloud Services including Anthos
### 1.Google Cloud IoT
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

**What is Anthos?**
- Google’s multi-cloud and hybrid cloud platform based on Kubernetes and Google kubernetes engine  
  + It's also a hybrid cloud because Anthers can manage Google clusters deployed within the Enterprise Data Center on premises.  

- Enables customers to run managed Kubernetes service (GKE) in a variety of environments

- Anthos can be deployed in  
  - Google Cloud  
  - vSphere (on-premises)  
  - Amazon Web Services  
  - Microsoft Azure  

- Non-GKE Kubernetes clusters can be attached to Anthos  
  + that means what happens if I have a cluster that is not a part of Anthos and it's already running and deployed some kubernetes clusters on prem in eight years in Asia or so on.  
  Now, even those Non-GKE Kubernetes clusters running outside of the context of Google cloud and the support environment, can also be technically attached to Anthos to be partially managed there.  
  + so you can not only lanuch and manage cluster, but also to register clusters were created outside of kubernetes running in any environment.

- Delivers centralized management and operations for Kubernetes clusters running diverse environments  
  + Anthos is like the gateway to managing multiple collaborative clusters no matter where they run.  

**Anthos Big Picture**
- two types of clusters:  
  + the managed GKE clusters that can native manage.  
  + unmanaged kubernetes clusters created outside of the realm of Anthos, for example.

- All these clusters can be managed by Anthos control plane.
  + once you register, you can do a lot of things with Anthos.

- **Anthos Services Mesh**
  +  give you an application centric network architecture  
     = secure the communication between micro services mean within communities.  
     = enforce network policies to protect your micro services  

- **Anthos config management**
  + a tool to deploy applications across all the registered clusters.  

- **Anthos Act Marketplace**
  + a catalog of various containerized applications and you can pick any application from the marketplace and deploy on any of the managed or unmanaged corporate clusters. e.g. apache server  

- **Ingress for Anthos**
  + a high level load balancer, which would make it easy for you to expose applications running on Anthos.  

- **Cloud Run**
  + like the platform as a service layer, a pass layer built on top of anthers so you can bring a container and walk away with a new URL.   

> Users will access the applications that are exposed by cloud run or ingress  
> while administrators are going to deal with Anthos via the config management and the marketplace.  

### 5.Demo
Purpose:how to register cluster's with Anthos.  
Two clusters:  
- one running within Google Cloud, which is a GKE   
- another cluster that is running in my laptop in my MacBook  
so register is the first step.

note
```
# Run the below commands in the macOS Terminal
# start by setting project ID
export PROJECT_ID=<PROJECT ID> # Replace this with your GCP project ID
export REGION=<REGION ID> # Replace this with a valid GCP region

# config project ID and define region
gcloud config set project $PROJECT_ID
gcloud config set compute/region $REGION

# Enable GKE related APIs
gcloud services enable \
     container.googleapis.com \
     gkeconnect.googleapis.com \
     gkehub.googleapis.com \
     cloudresourcemanager.googleapis.com

# Launch GKE Cluster (simple cluster with just one node)
gcloud container clusters create cloud-cluster \
    --machine-type=n1-standard-1 \
    --num-nodes=1
> now we have GKE cluster created called cloud-cluster, we can check on GUI.

# Launch Minikube.
minikube start
> Refer to the docs at https://minikube.sigs.k8s.io/docs/ ,helps you to lunch your own cluster on your machine.  
> We will have two k8s clusters, one is running in the cloud as a part of the investment, and the other one is basically the mini cub based cluster running on our laptop.

------register GKE Cluster------
# Create GCP Service Account(anthos-hub) before register our cluster
gcloud iam service-accounts create anthos-hub

# Add IAM Role to Service Account
gcloud projects add-iam-policy-binding $PROJECT_ID \
 --member="serviceAccount:anthos-hub@$PROJECT_ID.iam.gserviceaccount.com" \
 --role="roles/gkehub.connect"

# Download the Service Account JSON Key
gcloud iam service-accounts keys create "./anthos-hub-svc.json" \ --iam-account="anthos-hub@$PROJECT_ID.iam.gserviceaccount.com" \ --project=$PROJECT_ID
> this step is important because it's going to generate the JSON key

# Register cluster with Anthos
URI=` gcloud container clusters list --filter='name=cloud-cluster' --uri`

gcloud container hub memberships register cloud-cluster \
        --gke-uri=$URI \
        --service-account-key-file=./anthos-hub-svc.json

# List Membership
gcloud container hub memberships list
> if we check the Anthos we can see our GKE has been registered.

------Register Minikube with Anthosr------
# Register Minikube with Anthos
gcloud container hub memberships register local-cluster \
     --service-account-key-file=./anthos-hub-svc.json \
     --kubeconfig=~/.kube/config \
     --context=minikube
>This step will basically register our local minikube cluster with Anthos.
> we can also see the local cluster on the GKE but can't access the detail because we don't have the agent, the permission for Anthers to grab those detail.

# List Membership
gcloud container hub memberships list

---------------------------------------------
> give those permissions to the Anthos agent to greb local cluster details
> to enable us to talk to our local cluster, we need to create a community role and associate that with the agent running in the local cluster.

# Create Kubernetes Role
kubectl config use-context minikube

cat
<<EOF > cloud-console-reader.yaml
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: cloud-console-reader
rules:
- apiGroups: [""]
resources: ["nodes", "persistentvolumes"] verbs: ["get", "list", "watch"]
- apiGroups: ["storage.k8s.io"] resources: ["storageclasses"] verbs: ["get", "list", "watch"]
EOF

kubectl apply -f cloud-console-reader.yaml

# Create RoleBinding
> this cluster roll will make sure that the Anthos agent is able to talk to our local cluster.

kubectl create serviceaccount local-cluster

kubectl create clusterrolebinding local-cluster-anthos-view \
    --clusterrole view \
     --serviceaccount default:local-cluster

kubectl create clusterrolebinding cloud-console-reader-binding \
     --clusterrole cloud-console-reader \
     --serviceaccount default:local-cluster

# Get the Token
SECRET_NAME=$(kubectl get serviceaccount local-cluster -o jsonpath='{$.secrets[0].name}')
> now all these steps are done and what it actually gives us is a password that we can use.

# Copy the secret and paste it in the console
kubectl get secret ${SECRET_NAME} -o jsonpath='{$.data.token}' | base64 --decode
> now will be able to access the local cluster's details

----------------clean up--------------------

# Delete Membership
gcloud container hub memberships delete cloud-cluster
gcloud container hub memberships delete local-cluster

# Clean up
gcloud container clusters delete cloud-cluster --project=${PROJECT_ID}
     gcloud iam service-accounts delete anthos-hub@${PROJECT_ID}.iam.gserviceaccount.com
     minikube delete

```

### 6.Google Cloud Migration Tools
- Transfer Appliance  
  + can request from Google for an appliance that is going to contain all the data and you can ship it to Google for ingesting that into cloud storage or any of the target sources.

- Migrate for Compute Engine
  + based on a tool called velocerator that provides the capability of migrating existing virtual machines or even physical machines into GCE VMs.
  + this tool makes it easy for converting existing workloads and applications into a format that can be easily deployed on GCP.

- BigQuery Data Transfer Service  

**[For more products](https://cloud.google.com/products)**
