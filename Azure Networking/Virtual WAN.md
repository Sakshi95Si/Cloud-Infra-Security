# Azure Virtual WAN

---

Azure Virtual WAN (vWAN) is a managed networking service designed to simplify and optimize large-scale global network architectures. It integrates connectivity (VPN, ExpressRoute, SD-WAN), security, and routing into a unified hub-and-spoke model, ideal for enterprises with distributed resources across cloud and on-premises environments.

1. Hub-and-Spoke Architecture
   
* Hub: Central Azure-based network hub that connects:  
* Spokes: Virtual Networks (VNets), branch offices (via VPN/ExpressRoute), or partner SD-WAN devices.  
* Services: Built-in Azure Firewall, DDoS protection, and monitoring tools.  
* Enables global transit networking, allowing spokes to communicate through the hub.
  
2. Automated Scalable Connectivity
  
* Simplifies branch-to-cloud or branch-to-branch connectivity with auto-provisioning (e.g., VPN sites).  
* Supports thousands of branches with minimal manual configuration.
  
3. Integrated Security
   
* Azure Firewall: Centralized policy enforcement for traffic inspection (e.g., East-West and North-South).  
* Encrypted Connectivity: Site-to-site/IPsec VPN, ExpressRoute private links, and end-to-end encryption.
  
4. Partnership Ecosystem
   
* Integrates with SD-WAN partners (e.g., Cisco, VMware) for hybrid deployments.  
* Pre-validated appliances streamline connectivity to Azure.
  
5. Optimized Routing
  
* Dynamic (BGP) routing for efficient path selection.  
* Custom route tables to control traffic between VNets, branches, and services.

---

## Architecture Components:

1. Virtual WAN Instance: The global container for hubs, connections, and configurations.
   
3. Hubs  
* Regional Azure deployments acting as central routers (e.g., "West US Hub").  
* Each hub connects to: VPN Sites: Branch offices over IPSec VPN.  
* ExpressRoute Circuits: High-speed private connections.  
* VNets: Spoke networks in Azure.  
3. Connections  
* Branch (VPN): Connects on-premises sites via VPN gateways.  
* ExpressRoute: Dedicated private links for high-throughput workloads.  
* VNet: Attaches Azure VNets to the hub.  
4. Azure Firewall (Optional): Deployed in the hub for centralized security (L7 filtering, IDPS).

## Use Cases:

1. Global Enterprise Networks: Connect branch offices (retail stores, regional offices) to Azure and each other.  
2. Hybrid Cloud: Bridge on-premises data centers and Azure VNets with secure, low-latency links.  
3. Cloud-Native Applications: Enable microservices in multiple regions to communicate via a global backbone.  
4. Disaster Recovery: Failover between regions using optimized routing.

## Example Deployment:

\[Branch Offices (VPN)\]    
   ↓    
\[Azure vWAN Hub (East US)\] → \[Azure Firewall\]    
   |    
\[Spoke VNets (App, DB)\]    
   |    
\[ExpressRoute → On-Premises DC\]  

* Traffic Flow: Branch offices connect via VPN to the hub, which routes traffic to Azure VNets or on-premises via ExpressRoute. Azure Firewall inspects and filters traffic.

---

## When to Use Azure Virtual WAN:

* Complex Networks: Multiple branches, hybrid cloud, or global applications.  
* Simplified Operations: Reduce manual configuration with automation.  
* Security Needs: Centralized Zero Trust policies and traffic inspection.

## Limitations & Considerations:

* Cost: Hub pricing includes gateway and data processing fees.  
* Region Availability: Hubs are region-specific; deploy multiple for global coverage.  
* Partner Integration: Requires compatible SD-WAN appliances for hybrid setups.

