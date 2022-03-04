### APP Engine [more info](https://cloud.google.com/appengine/docs/the-appengine-environments)  
- One of the first compute services from Google (PaaS)   

- Fully managed platform for deploying web apps at scale
  + Fully managed means that user don't have to deal with provisioning, configuring, scaling, managing and securing the platform or infrastructure.
  + Automatically scale the application as request increase.
  + The code will runs in the same context of Google's infrastructure.   

- Supports multiple languages, frameworks, and libraries

- App Engine is available in two environments   
  + Standard   
  + Flexible(complete control over packaging and deployment)  

- Applications deployed in standard environment run in a sandbox   

- Flexible environment uses Docker containers to deploy and scale apps


### Compute Engine(Laas - VM - Highly customized workloads )
- Give you a choice of virtual machines with a different set of configurations where you take control by logging into the VM installing the software of your choice and treating it like a machine.  

- GCE enables Linux and Windows VMs to run on Google’s global infrastructure  

- VMs are based on machine types with varied CPU and RAM configuration

- Persistence is available through standard and SSD disks  
  + if you start a vm and have a local disk attached to it you install some software you configure that and then terminate it you lose all the changes and all the configuration that you have made to the machine if you want to bring persistence then you need to attach additional storage.   

- VMs are charged a minimum of 1 minute and in 1 second increments after that  

- **Sustained use discounts** are offered for running VMs for a significant portion of the billing month   

- **Committed use discounts** are offered for purchases based on 1 year or 3 year contracts(long-term-discounts)


### Kubernetes Engine    
- All about an orchestration platform.  

- Fundamental shift that is happening in the infrastructure segment, virtual machines are slowly getting replaced by containers.    

- A platform it's an orchestration engine to manage tens of thousands of containers that are deployed in the cloud.    

- GKE is a managed environment for deploying containerized applications managed by Kubernetes
  + You can bring in your container images, and package them as the kubernetes artifacts deploy them and scale them through GK kubernetes.  

- Kubernetes has a control plane and worker node  
  + it's a typical distributed computing environment where you have the control plane managing the worker node or the data plane that is running the multiple set of worker nodes.  

- GKE provisions worker nodes as GCE VMs  
  + when you launch a cluster in google kubernetes engine there are **two elements one is the control plane the other one is a data plane**  
  + Google takes care of the control plane or the master nodes that are responsible for managing the entire cluster.  

- Node pools enable mixing and matching different VM configurations  
  + a node pool is a collection of homogeneous VMs that deliver either high memory or high storage throughput or high CPU environment.  

- The service is tightly integrated with GCP resources such as networking, storage, and monitoring  
  + Monitoring is responded by Stackdriver, a the built-in monitoring and tracing platform.  

- Auto scaling, automatic upgrades, and node auto-repair are some of the unique features of GKE  


### Cloud Functions  
- Represents functions as a service.      
- Cloud Functions is a **serverless** execution environment for building and connecting cloud services  
  + Write code as a service  
  + no need to provision a virtual machine or a container.

- Serverless compute environments execute code **in response to an event**
  + oinstead of running this code forever they get executed only when there is an external event   
  + e.g. adding a new object to a storage bucket  

- Cloud Functions supports JavaScript, Python 3, and Go  

- GCP events fire a Cloud Function through a trigger  
  + trigger is what connects the external resource to a cloud function.  
- An example event includes adding an object to a storage bucket  

- Trigger connects the event to the function

### Demo
```
# logging to the project environment
gcloud config set project <project ID>

# after creating the instance
gcloud compute instances list

# ssh to instance
gcloud compute ssh <instance name> --zone <zone name>
gcloud compute ssh instance test --zone asia-northeast1-b

# GCP is going to add some metadata based on the SSH keys so it's going to inject an ssh public key into the vm and creates a private key. one command will create the ssh infrastructure required for you to log into the vm.

passphrase: Lee

# After enter the pass, now we in the VM.
# Update the packages to refresh the packages and speed up the installation of Apache web server.
sudo apt-get update

# install Apache2
# this will install all the dependencies and configure our machine for the webserver
sudo apt-get install -y apache2

# start the Apache service
sudo systemctl start Apache2

# click address on the instance

```
