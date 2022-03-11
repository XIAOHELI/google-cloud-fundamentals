### Overview of Google Cloud devOps Services
- DevOps Services provides tools and frameworks for automation  

- Cloud Source Repositories store and track source code  

- Cloud Build automates continuous integration and deployment  
  + + a CI-CD service provided by Google it can integrate with either cloud source repositories or third-party repositories like GitHub and GitLab.  
  +  CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment. e.g. GitHub...

- Container Registry acts as the central repository for storing, securing, and managing Docker container images  

- IDE and tools integration enables developer productivity  

### 1. Source Repositories
- Acts as a scalable, private Git repository  

- Extends standard Git workflow to Cloud Build, Cloud Pub/Sub and Compute services  

- Unlimited private Git repositories that can mirror code from Github and Bitbucket repos  

- Triggers to automatically build, test, and deploy code  

- Integrated regular expression-based code search  

- Single source of code for deployments across GCE, GAE, GKE, and Functions  
  + advantage of using cloud source repos is to maintain single source of code repository for deployment across multiple compute functions provided by GCP.  

### 2. Cloud Build  
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
  
###
