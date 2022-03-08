
###  Overview of Google Cloud Network services[Details](https://cloud.google.com/network-tiers/docs/overview)
-  Network services are one of the key building blocks of cloud  

-  GCP leverages Google’s global network for connectivity  

-  Customers can choose between standard and premium tiers
    + offer a trade-off between performance and cost.  

-  Load balancers route the traffic evenly to multiple endpoints
    + route the traffic evenly to multiple applications or multiple instances of the applications.

-  Virtual Private Cloud (VPC) offers private and hybrid networking  

-  Customers can extend their data center to GCP through hybrid connectivity  


### 1.GCP Network Service Tiers
-  Network service tiers provide a choice of traffic optimization   
-  There are two service tiers:  
  + Premium Tier   
  + Standard Tier
-  Premium Tier delivers traffic via Google's premium backbone
    + powers the rest of google services like google search, gmail, g-suite, youtube and so on  

-  Standard Tier uses regular connectivity based on ISP networks  
    + used regular connectivity based on isp networks  
    + based on third party connectivity and doesn't use the high throughput and high performance network backbone, hence standard tier is obviously cheaper.  

-  GCP uses premium tier as the default option  

### 2.Google Cloud Load Balancing
-  Load balancer distributes traffic across multiple GCE VMs in a single or multiple regions  

-  There are two types of GCP load balancers:   
  +  HTTP(S) load balancer -> global  
  +  Network load balancer -> same region  

-  **HTTP(S) load balancer provides global load balancing**
    + typically meant for routing traffic to web apps that are deployed in more than 1 zone or more than 1 region.

-  Network load balancer balances regional TCP and UDP traffic  
    + routing the traffic across multiple tcp and udp end points but within the same region.

-  **Both types** can be configured as internal or external load balancers  
    + you can use a combination of both external and internal to achieve maximum scale-ability and better performanc.  

#### 2.1 architectural diagram
- 1. mobile app or web app that is actually using an external load balancer so you have multiple users in US and Asia.  
- 2. first hitting the external load balancer and from there the traffic gets routed to one of the regions that is US central 1b and Asia east 1a so depending on where the user is coming from.  
- 3.role of the http load balancer is to route the traffic to the appropriate location.  
- 4.once the traffic hits the web tier in one of the locations then it needs to talk to the database via a set of app servers. Since there are multiple app servers, that is, more than 1 app server also needs to be front ended with a load balancer. web tier talks to the app tier which is an internal tier via a load balancer which is called an internal load balancer.  

### 3.Virtual Private Cloud
-  VPC is a software defined network providing private networking for VMs  
    + isolates the VMs running inside the VPC with rest of the world.

-  VPC network is a global resource with regional subnets  
    + means you create a VPC that is visible from any of the regions that you have within GCP and beyond that, you can create a subnet per region that is going to be attached to the same VPC and provide lot of flexibility.

-  Each VPC is logically isolated from each other  
    + one of the core requirements of virtual private cloud or hybrid cloud so one VPC cannot see the resources deployed in another VPC because each VPC is completely running in its own isolated environment. so even if you are creating multiple VPCs you need to explicitly allow communication between these VPCs by creating firewall rules.  

-  Firewall rules allow or restrict traffic within subnets  
    + it is quite common for customers to create a public subnet and multiple private subnets and keep sensitive resources within the private subnets and private subnets are never exposed to the outside world only those resources deployed in the public subnet become visible to the outside world and they act as the channel to talk to the resources.  

-  Resources within a VPC communicate via IPV4 addresses  

-  VPC networks can be connected to other VPC networks through VPC
peering  
    + if you are running multiple VPCs and you may want to share resources among them you can create a VPC peering, which will bring one or more VPCs together and it becomes a logical extension of the VPCs in order to share the resources with each other.

-  VPC networks are securely connected in hybrid environments using Cloud VPN or Cloud Interconnect  
    + VPC is the basic requirement for enabling hybrid cloud connectivity between your on-prem data center and GCP public cloud.  
    + by using the VPC networks through cloud VPN or cloud interconnect, we can achieve a private communication between your data and the resources running in the public cloud.  

### 4.FCP Hybrid Connectivity[more info](https://cloud.google.com/hybrid-connectivity/)  
-  Hybrid connectivity extends local data center to GCP  

-  Three GCP services enable hybrid connectivity:   
  +  Cloud Interconnect  
  +  Cloud VPN  
  +  Peering  

-  Cloud Interconnect extends on-premises network to GCP via Dedicated or Partner Interconnect  
  + when you are considering connecting your local data center to the cloud you can choose between Google's own network that is spread across the globe, or you could use one of the partners that Google designates for enabling the interconnectivity.  

-  Cloud VPN connects on-premises environment to GCP securely over the internet through IPSec VPN  
  + this is very affordable very economical mechanism to extend your data center because you are **not using a dedicated network provided by Google or their partners instead you choose public internet over VPN.**  

-  Peering enables direct access to Google Cloud resources with reduced Internet egress fee  
  + Google has partnered with a lot of ISPs and data center providers, and, by tapping into one of those partner networks, you can enable direct access so when compared to interconnect, peering gives you a much lower egress fee. egress fee is the bandwidth that you are charged for outbound connectivity so when you are making requests to the cloud from your data center we are pairing there is an egress fee but this is much lower when compared to cloud interconnect.  

### 5.Demo - configuring Load Balancing
```
# 1.Dashboard
-----------create instance template--------------
# 2.go to Compute Engine -> instance templates
the demo that we are going to configure is a couple of VMs deployed in a region. currently, a load balancer where the traffic is routed evenly across the instances so when we are launching the VMs instead of creating them independently, and configuring them with exactly the same settings and same software. we can create an instance template as a group blueprint to be used to launch multiple GC VMs at one time.

# 3.choose configuration

# 4.enable Http traffic to run a web server

# 5.Management-> start up script
#! /bin/bash
apt-get update
apt-get install -y apache2
cat <<EOF > /var/www/html/index.html
<html><body><h1>Hello from $(hostname)</h1>
</body></html>
EOF

# 6.create the template

-----------create instance group--------------
# 7.go to instance groups ->create
every configuration that we have used for the template will be automatically used by the group.

# 8.create a health check
check interval is 10 seconds now what this means is every time the load balancer tries to send the traffic it checks the health status.

# 9.change the initial delay to send a green signal for the load balancer to route the traffic within a minute.

# 10.create

-----------check instances--------------
# 11.check instances -> click the External IP
these instances have default external IPS the public IPS and clicking on these will show us hello from the hostname which is the unique name assigned to each of the VMs.

-----------create load balancer--------------

now we notice that the output from each of these web servers is different and unique. so when we configure the load balancer and start hitting the load balancer from a browser, we are going to see the traffic getting evenly sent to one of these web servers.

# 12. go to network services -> Load balancing
we have the GCE infrastructure in place we have two instances running with two external IPS so let's go to the network section and clear the load balancer.

# 13.choose HTTP load balancing because we are talking to a web application back-end.

# 14.create backend configuration
create backend services, we can choose Network endpoint groups if you are running individual VMs. but since we already have an instance group we choose the back-end type as the instance group.

choose the webserver instance group we have launched in the previous step. the port is 80 that is the default port on which Apaches is listing. balancing mode is very important whether you want to route the traffic based on CPU utilization or the requests per second.

associate this back-end with the health check we created earlier, so if the health check fails for one of the instances, the load balancer will gracefully send the request to the other instance enhance user experience.

# 15.Host and path rules
Since we don't have multiple endpoints we'll leave that as the default.

# 16.Frontend configuration
Create and it takes a couple of more minutes for the webserver to be completely configured and the health check to pass, the load balancer will be able to route the traffic to one of the instances in the backend group based on the instance template that we created.

# 17.click the load balancer's link
then we see that it's been assigned a public IP address and available on port 80 you can also see that the healthy status shows two of two which means both the web servers are now available and they are healthy.

now we can verify the functionality of this load balancer by copying this IP address and accessing it from the browser so one of the web servers is responding and you can notice that the hostname is unique now as we start refreshing. we'll actually see that the traffic is evenly routed among these instances.

# Summarize
we first launched an instance template configured the VM configuration, then from that instance, we created a group and this group had two GC VMs launched in two different availability zones. we also created a health check to make sure that the health is always checked periodically and reported back to the load balancer. within the GCE environment, we switch to the network services and configure the load balancing within the load balancing, we have the backend which is pointing to the instance group associated with the health check, then we created the front-end which is nothing but the ephemeral IP address and the port is exposing the load balancer and we connected the front end to the backend after the health check has been performed. once everything is green we got the public IP address and when we access that the traffic is evenly routed to one of the instances.

```

### 6. Use Cases of GCP Network Services
check the diagram
