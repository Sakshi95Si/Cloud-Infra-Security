**Azure Virtual Network**

---

![diag](https://github.com/Sakshi95Si/Cloud-Infra-Security/blob/main/Azure%20Networking/Vnet.png)

* Azure virtual network(Vnet) is a logical representation of an isolated network.  
* Creates a dedicated private cloud only Vnet.  
* Securely extend your data centre with Vnets.  
* Enable hybrid cloud scenarios.  
* Layer-3 construct, understands IPs,TCP,UDP,ICMP etc (No VLANs).  
* It's a software defined network, you cannot broadcast or multicast.  
* Cannot span a particular subscription and region.   
* Is not pinned to a certain availability zone.

**Subnets**

* A virtual network can be segmented into one or more subnets.  
* Subnets provide logical divisions within your network.  
* Subnet can help improve security, increase performance and make it easier to manage the network.  
* Each subnet must have a unique address range and cannot overlap with other subnets in the virtual network.

---

**Subnet Considerations/Requirements:**

1. Service requirement  
     
   Each service directly deployed into Vnet has specific requirements for routing and the type of traffic that must be allowed into and out of the subnets. A service may require or create their own subnet so there must be enough under linkage of space for them to do so.  
     
2. Virtual appliances  
     
   Azure route network traffic between all subnets in the Vnet by default, you can override default routing between subnets or can route traffic from Vnet to a network virtual appliance.  
     
3. Service Endpoints  
     
   You can limit access to resources such as Azure storage account or Azure SQL database to specific subnet with a virtual network service endpoint.

\*\*\*Azure reserves 5 IPs in a subnet range.

0 \- network address IP  
1 \- default gateway IP  
2 \- DNS  
3 \- DNS  
.  
.  
.  
255 \- network broadcast

---

**Implementing virtual networks:**

1. You create a virtual network when you create a virtual machine in azure.  
2. Need to define the address space, and at least one subnet.   
3. Be careful with overlapping address spaces.  
4. By default you can create up to 50 Vnets per subscription and region, but the limit can be increased by contacting the support.  
5. Always plan to not use address spaces that are already present in your organisation.

