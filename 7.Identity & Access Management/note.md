###  Overview of IAM
- IAM controls access by defining **who**(identity) has **what** access (role) for **which** resource.

- Cloud IAM is based on the principle of least privilege  
  + which means by default all the resources are denied access and you are expected to open up access explicitly.   

- An IAM policy binds identity to roles which contains permissions  
  + it essentially means is that there are a set of permissions and these permissions are grouped together into a role, and that role is assigned to a member, and the member would automatically inherit all the permissions.  

  + roles are nothing but a collection of permission.  
  + these roles are applied to the members the member identity.  
  + policy is what is binding the member identity and a role together.  

### 1.Cloud IAM Identity
- Google account  
- Service account: a service account is a special type of user it is not associated with a user or member directly but it is meant for applications to talk to GCP resources.  
- Google group:it represents a logical entity thats a collection of users.  
- G Suite domain  
- Cloud Identity domain     
- all Authenticated Users:if you want to provide a blanket access to all the resources for any authenticated user by google, you can use this alias.     
- allUsers:this even to anonymous users you can use the alias.    

### 2.Cloud IAM Permissions
- Permissions determine the operations performed on a resource  

- Correspond 1:1 with REST methods of GCP resources  

- Each GCP resource exposes REST APIs to perform operations  
  + Google cloud platform is based on a collection of api's so every GCP resource has multiple API is associated with it permissions.  

- Permissions are directly mapped to each REST API  
  + Publisher.Publish() -> pubsub.topics.publish

- Permissions cannot be assigned directly to members/users  

- One or more permissions are assigned to an IAM Role  
  + it's also important to understand that permissions are mapping to rest api's exposed by GCP resources  

### 3.Cloud IAM Roles
- all roles are nothing but a collection of permissions, it's a logical grouping of various permissions so there could be three types:  

- Primitive roles  
  + Owner: 100% access to the resource  
  + Editor: modify and add additional permissions  
  + Viewer: only read-only access to the resource  

- Predefined roles
  + roles/pubsub.publisher  
  + roles/compute.admin  
    + for example compute admin is a role that has all the relevant permissions to manage compute engine instances.  
  + roles/storage.objectAdmin  

- Custom roles  
  + Collection of assorted set of permissions  
  + Fine-grained access to resources  

### 4.Cloud IAM Key Elements
- Resource – Any GCP resource  
  + Projects  
  + Cloud Storage Buckets  
  + Compute Engine Instances  

- Permissions - Determines operations allowed on a resource  
  + <service>.<resource>.<verb>: Permission structure  
  + pubsub.subscriptions.consume: To consume or to subscribe to a pub sub topic.  
  + compute.instances.insert  

- Roles – A collection of permissions
  + Compute.instanceAdmin  
    = compute.instances.start  
    = compute.instances.stop  
    = compute.instances.delete   
    = ....  

- Users – Represents an identity
  + Google Account  
  + Google Group  
  + G Suite Domain  
  + ...

### 5.Demo - Members, Roles, Permissions
```
------create role--------
# go to IAM Dashboard
# check Roles
# create new role with the permission  

-----Add member to the role-------
# go to IAM and click ADD on the TOP
# Add new member
# select role -> custom -> created role by us above

# check ROLES
```

### 6. Service Accounts
- A special Google account that belongs to an application or VM
  + it doesn't represent and identity directly but this identity is enabling an application or VM to access Google cloud resources. imagining you have an application running inside GCE and that needs to programmatically create resources or talk to the Google cloud platform API you still need permissions to do that and that's where a service account comes in very handy.   

- Service account is identified by its unique email address  
  + service account is identified by a unique email address assigned by GCP you don't have control on how that is being created it uses a combination of your project identifier.  

- Service accounts are associated with key-pairs used for authentication  
- Two types of service accounts   
  + User managed  
  + Google managed  
- Each service account is associated with one or more roles  

### 7. Demo - Cloud IAM Service Accounts
```
# go to Service Account

# create a service account

# assign roles

# create keys
click on create this is going to generate a JSON file and gets automatically downloaded, so when you open the JSON file in an editor you see that it has a private key and it has the complete identity information related to the service account. so Google exposes API for applications that can read this information and can use the private key available within the service account programmatically to talk to the resources.


```

### 8.When to use IAM
- To share GCP resources with fine-grained control  
- Selectively allow/deny permissions to individual resources  
- Define custom roles that are specific to a team/organization  
- Enable authentication of applications through service accounts  
