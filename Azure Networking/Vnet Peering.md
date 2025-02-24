# Azure Vnet Peering

---

Azure Virtual Network peering lets you connect virtual networks in the same or different regions. Azure Virtual Network peering provides secure communication between resources in the peered networks.

* There are two types of Azure Virtual Network peering: regional and global.


![Diag](https://github.com/Sakshi95Si/Cloud-Infra-Security/blob/main/Azure%20Networking/peer.png)


* Regional virtual network peering connects Azure virtual networks that exist in the same region.  
* Global virtual network peering connects Azure virtual networks that exist in different regions.  
* You can create a regional peering of virtual networks in the same Azure public cloud region, or in the same China cloud region, or in the same Microsoft Azure Government cloud region.  
* You can create a global peering of virtual networks in any Azure public cloud region, or in any China cloud region.  
* Global peering of virtual networks in different Azure Government cloud regions isn't permitted.  
* After you create a peering between virtual networks, the individual virtual networks are still managed as separate resources.

**Benefits:**

* Network traffic between peered Vnets is private, no public internet, gateways or encryption is required in communication between these Vnets.  
* Low latency high bandwidth connection between resources and different Vnets.  
* Seamless: the ability to track data across Azure subscription, deployment models and across azure regions.  
* No disruption or no downtime of resources in Vnets when peered. 

---

**Gateway Transit And Connectivity**

* A virtual network can have only one VPN gateway.  
* Gateway transit is supported for both regional and global virtual network peering.  
* When you allow VPN gateway transit, the virtual network can communicate to resources outside the peering. In our sample illustration, the gateway subnet within the hub virtual network can complete tasks such as:  
1. Use a site-to-site VPN to connect to an on-premises network.  
2. Use a vnet-to-vnet connection to another virtual network.  
3. Use a point-to-site VPN to connect to a client.  
* Gateway transit allows peered virtual networks to share the gateway and get access to external resources. With this implementation, you don't need to deploy a VPN gateway in the peered virtual network.  
* You can apply network security groups in a virtual network to block or allow access to other virtual networks or subnets. When you configure virtual network peering, you can choose to open or close the network security group rules between the virtual networks.

![Diag](https://github.com/Sakshi95Si/Cloud-Infra-Security/blob/main/Azure%20Networking/gatewaytransit.png)

**Service Chaining**

* Leverages user defined route to implement custom routing.  
* Implement a Vnet hub with a network virtual appliance or a VPN gateway.  
* Service chaining enables you to direct traffic from one Vnet to a virtual appliance or Vnet gateway in a period network through user defined routes.

