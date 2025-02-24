# Azure Routing

---

Routing in Azure determines how network traffic flows between resources in your Azure Virtual Networks (VNets), on-premises networks, and the internet. Azure provides both default routing and tools to customize routing for complex scenarios. 

## 1\. Default Routing in Azure

When you create a VNet, Azure automatically configures system routes to handle basic traffic. 

These routes are invisible but govern traffic flow by default:

* Local VNet Traffic: Direct communication between resources in the same VNet.  
* VNet Peering: Traffic between peered VNets (if peering is configured).  
* Internet Traffic: Outbound traffic to the internet (via the VNet’s default route).  
* On-Premises Traffic (Hybrid Networks): Routes to on-premises networks via VPN/ExpressRoute (if connected).  
* Service Endpoints: Traffic to Azure services (e.g., Azure Storage, SQL DB) stays within Azure’s backbone (no public internet).

## 2\. Custom Routing with User-Defined Routes (UDRs)

To override default routing, use User-Defined Routes (UDRs). UDRs let you define custom paths for traffic, such as forcing traffic through a firewall, VPN gateway, or Network Virtual Appliance (NVA).


**How UDRs Work:**

* Create a Route Table: Define rules (routes) in a table.  
* Associate the Route Table: Attach it to a subnet (e.g., your application subnet).  
* Define Routes: Specify:  
  Address Prefix: Destination IP range (e.g., 10.1.0.0/16 for on-premises).  
  Next Hop Type: Where to send the traffic (e.g., Virtual Appliance, VPN Gateway, Internet).

 
## 3\. Border Gateway Protocol (BGP) for Hybrid Networks

For hybrid setups (Azure \+ on-premises), BGP dynamically exchanges routing information between Azure VPN/ExpressRoute and your on-premises routers. This allows:

* Automatic Route Updates: New subnets in Azure are advertised to on-premises.  
* Path Selection: Choose the best route based on network policies.

## 4\. Azure Route Server

For advanced scenarios, Azure Route Server lets network appliances (e.g., Cisco, Palo Alto) exchange routes dynamically with Azure. This simplifies hybrid cloud routing without manual UDRs.

---

## Key Scenarios

* Forced Tunneling  
  What: Redirect all internet-bound traffic to an on-premises network (e.g., for compliance).  
  How: Create a UDR with 0.0.0.0/0 pointing to your VPN/ExpressRoute gateway.  
    
* Hub-and-Spoke Topology  
  Hub VNet: Hosts shared services (firewall, VPN gateway).  
  Spoke VNets: Route traffic through the hub using UDRs.  
  Example: Spoke subnets send traffic to the hub’s firewall for inspection.  
    
* High Availability with Multiple NVAs  
  Use Azure Load Balancer to distribute traffic across multiple NVAs (e.g., firewalls) and define UDRs pointing to the load balancer’s IP.  
  

---
  
## How to View Effective Routes

Check the effective routes for a network interface (NIC) to see combined system/UDR/BGP routes:

* Go to the VM’s NIC in the Azure Portal.  
* Under Support \+ troubleshooting, select Effective routes.

## Common Pitfalls

* Overriding Default Routes: Ensure UDRs don’t block critical traffic (e.g., Azure LB health probes).  
* Route Precedence: UDRs override system routes. BGP routes (if used) override UDRs.  
* Circular Routing: Misconfigured UDRs can cause traffic loops (e.g., routing between NVAs indefinitely).  
* Overlapping Address Spaces: Conflicting IP ranges break routing.

## Example: Hub-and-Spoke Routing

* Hub VNet: Contains a firewall (NVA) at 10.0.1.4.  
* Spoke VNet: Subnet 10.1.0.0/24 hosts web servers.  
* UDR in Spoke:  
  Destination: 0.0.0.0/0 → Next Hop: 10.0.1.4 (Firewall)  
  Destination: 10.0.0.0/16 → Next Hop: VNet Peering (Hub)  
  Result: All internet and cross-VNet traffic flows through the firewall.  
  

