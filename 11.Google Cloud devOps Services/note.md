### Overview of Google Cloud devOps Services
- DevOps Services provides tools and frameworks for automation  

- Cloud Source Repositories store and track source code  
  + e.g Github...

- Cloud Build automates continuous integration and deployment  
  + + a CI-CD service provided by Google it can integrate with either cloud source repositories or third-party repositories like GitHub and GitLab.  
  +  CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment.

- Container Registry acts as the central repository for storing, securing, and managing Docker container images  

- IDE and tools integration enables developer productivity  

> Google Cloud source code repo will store your your source code while cloud built is going to be responsible for building and packaging your applications and container registry is going to store the docker images and the artifacts in a centralized registry.

centralized registry
### 1.Source Repositories
- Acts as a scalable, private Git repository  

- Extends standard Git workflow to Cloud Build, Cloud Pub/Sub and Compute services  

- Unlimited private Git repositories that can mirror code from Github and Bitbucket repos  

- Triggers to automatically build, test, and deploy code  

- Integrated regular expression-based code search  

- Single source of code for deployments across GCE, GAE, GKE, and Functions  
  + advantage of using cloud source repos is to maintain single source of code repository for deployment across multiple compute functions provided by GCP.  

### 2.Cloud Build  
- Managed service for source code build management  

- The CI/CD tool running with Google Cloud Platform  

- Supports building software written in any language  

- Custom workflow to deploy across multiple target environments  
  + means with cloud build you can take existing source code repositories and build them, and package the code targeting virtual machines or containers or serverless functions.

- Tight integration with Cloud Source Repo, GitHub, and Bitbucket  
  + this is going to be the source for your code repositories and they act as the initial phase for triggering the entire CI CD pipeline.

- Supports native Docker integration with automated deployment to Kubernetes and GKE  
  + if you are running GKE or a kubernetes cluster on top of GCE you can use cloud build to package and deploy containerized applications to one of these environments.

- Identifies vulnerabilities through efficient OS package scanning  
  + ensure that your source code is free of any vulnerabilities and threats. You also can package the application that is free of any other vulnerabilities that are typically found with operating system packages or through the third-party libraries.

  Google Cloud build takes the source code stored either in source code repo of GCP or bitbucket gitlab or github and creates the integration and deployment pipeline. The target and the destination environment could be any of the supported computer environments but this is the bridge between your source code repo and your deployment target.


### 3.Container Registry
- Single location to manage container images and repositories

- Store images close to GCE, GKE, and Kubernetes clusters  

- Secure, private, scalable Docker registry within GCP  

- Supports RBAC to access, view, and download images  

- Detects vulnerabilities in early stages of the software deployment

- Supports automatic lock-down of vulnerable container images
  + so in case a vulnerability is found after the container image has been stored, it can even be locked down to prevent it from getting into your production deployments. This will isolate any identified container images with vulnerabilities or threats.

- Automated container build process based on code or tag changes  
  + so in the CI CD pipeline you first have the source code repos, then you have the build service. And the outcome of build typically ends up in the container registry so cloud build might actually build docker image which is going to be stored in the centralized registry provided by Google container registry. From there, it finds its way to the target which could be one of the containerized compute environments like GCE, GKE or a custom kubernetes cluster running within GCP.  

### 4.Integration with Developer Tools
- IDE plugins for popular development tools   
  - IntelliJ  
  - Visual Studio   
  - Eclipse  
- Tight integration between IDEs and managed SCM, build services   
- Automates generating configuration files and deployment scripts   
- Makes GCP libraries and SDKs available within the IDEs  
- Enhances developer productivity  

### 5.Demo
The demo for this section is storing images in container registry by taking a docker file build the image and push it to Google Cloud container registry.

> search for container registry
> currently we don't have any images stored in the repository because we haven't built a container at we haven't built a container image it and we haven't pushed it to GCR which is Google container registry.

> so let's look at this set of commands that we need to execute to create a custom docker image and store it in container registry.


```
Lab Guide for Google Container Registry

# enter Shell
gcloud config set project <project ID>

# Run the below commands in Google Cloud Shell to enable API
gcloud services enable containerregistry.googleapis.com

# once API enabled
export PROJECT_ID=<PROJECT ID> # Replace this with your GCP Project ID
export PROJECT_ID=fast-ability-343009

# docker version
docker version

# check if we have images locally
docker images

# pull the busybox image
docker pull busybox
docker images

# create docker file
vim Dockerfile
-----
from busybox:latest
CMD ["date"]
-----

# build the image
# call as my busybox, this is going to take the busybox and build a custom image based on the docker file that we have currently created.
docker build . -t mybusybox
docker images

# we tag it to ensure we are following the convention expected by GCP container registry. so we call it gcr.io
docker tag mybusybox gcr.io/$PROJECT_ID/mybusybox:latest

# check and we will notice that the same image has been tagged with the convention expected by GCP
docker images

# check to see if it will run as we expected
docker run gcr.io/$PROJECT_ID/mybusybox:latest

# This will basically link the GCP container registry with docker so
that we can continue to use the docker CLI. Normally, it will automatically registered.
gcloud auth configure-docker

# finally, run push the entire image to the container registry.
docker push gcr.io/$PROJECT_ID/mybusybox:latest

# refresh on the page and we can see the box is there.
so once the image is stored in the container registry, you can pull this from a pod running in kubernetes engine or another docker application running inside compute engine. it doesn't matter where you are using this but you can very quickly pull this from your applications such as app engine flakes or kubernetes Engine or compute engine.
```

> 1 we start off by enabling the api's so every service that Google exposes as a part of GCP has an API associated with it. And even before we can use the command-line tools against those services, we still need to enable the appropriate API.

> 2 that we initialize an environment variable and set it to the project ID.

> 3 we use the docker pull command to basically pull the tiny linux image called busybox then we go ahead and customize it.

> 4 two lines commands (from busybox:lates CMD ["date"]) add into the docker file is all we need to build our image, the image will simply print the "date" when we run it.

> 5 after we build the docker image, we tag it appropriately based on the convention that GCP uses.

> 6 so gcr.io is the prefix that we need to use when we are using docker images stored within the container registry followed by the project ID that we have initialized in the environment variable. And we are calling this my busybox and adding a tag called latest. so we rename it literally tagging is nothing but renaming and then we test the local image that we have just built by running docker.

> 7 we run this command called "configure docker" which associates the GCP credentials with docker CLI so that we can directly use docker push against the container registry.

# 6. use cases -> see PDF
