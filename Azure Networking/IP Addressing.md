# IP Addressing

---

IP addresses are of two types: private and public.

1. **Private IP**: Used within an Azure virtual Network and your on-premises network,or when you use a VPN gateway or Express route circuit to extend your network to Azure.  
2. **Public IP**: Used for communication with the internet, including Azure public facing services.

![Azure Networking/IP.png](https://github.com/Sakshi95Si/Cloud-Infra-Security/blob/main/Azure%20Networking/IP.png)

IP addresses are further classified into Static and Dynamic IPs.

1. **Static IP**:  Do not change and you can select and assign any unassigned or unreserved IP address in the subnet's address range, this is ideal for certain situations example-  
* DNS name resolution where a change in an IP address would require updating host records.  
* Certain applications and services which require static IP.  
* SSL certificate linked to IP addresses.  
* Firewall rules that allow / deny traffic using IP address range.

Static IP address is assigned when a public IP address resource is created.

* IP address is not released until the public IP resource is deleted.  
* If the address is not associated with a resource you can change the assignment method after the address is created.  
* If the address is associated with a resource you cannot change the assignment method.

2. **Dynamic IP**:  Changes when the resource it is assigned to is switched off and on.  
* Private IPs are normally dynamic.  
* Dynamic addresses are assigned only after the public IP address is associated with an azure resource and the resource is started for the first time.   
* Dynamic addresses are released when a public IP address resource is disassociated from a resource it is associated with.  
* Azure assigns the next available unassigned or unreserved IP address in the subnet's address range.

\*\*\* IP addresses are never managed from or within the virtual machine in Azure. 


---


**Creating Public IP address:**

* Available in IPv4 or IPv6 or both.  
* Basic and Standard Sku.  
* Available in dynamic, static or both depending on the Sku.  
* Zone redundant.  
* Not mixable or immutable.  
* Range of contagious addresses available as a prefix.  
* Sku cannot be changed after public IP is created.   
* If selecting IPv6 then the assignment method must be dynamic for basic Sku.  
* Standard Sku addresses are static for both IPv4 and IPv6. 

**Basic Sku:**

* Open by default.  
* Free, dynamic or static.  
* No availability zone support.

**Standard Sku:**

* Locked down by default.  
* Not free, static only.  
* Zone redundant by default.
