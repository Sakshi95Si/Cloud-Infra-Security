# Azure Hybrid Network Connectivity
---

Azure Hybrid Network Connectivity enables seamless and secure communication between on-premises networks (data centers, branch offices) and Azure cloud resources (Virtual Networks/VNets). It bridges your existing infrastructure with Azure services, supporting scenarios like cloud migration, disaster recovery, and hybrid applications.

## Key Components & Services:

1. **Azure VPN Gateway**

* Establishes site-to-site (S2S) VPN tunnels over the public internet using IPSec/IKE protocols.  
* Point-to-Site (P2S) for individual device connectivity (e.g., remote employees).  
* Supports active-active or active-passive configurations for high availability.

2. **Azure ExpressRoute**

* Provides private, dedicated network connections via a connectivity partner (e.g., AT\&T, Verizon).  
* Bypasses the public internet for higher reliability, lower latency, and guaranteed SLAs (99.95%–99.99%).  
* ExpressRoute Global Reach connects on-premises sites across regions via Azure’s backbone.  
    
3. **Azure Virtual WAN**

* Simplifies large-scale hybrid networking by integrating VPN, ExpressRoute, and SD-WAN.  
* Centralizes connectivity for branch offices, VNets, and on-premises networks.  
    
4. **Azure Virtual Network (VNet)**  
     
* The foundation for Azure resources, connected to on-premises via VPN/ExpressRoute.  
    
5. **Azure Bastion**

* Securely access VMs over SSL without exposing public IPs.

---

## Hybrid Connectivity Options:

| Feature | VPN Gateway | Express Route | Virtual WAN |
| :---- | :---- | :---- | :---- |
| Connection type | Encrypted over internet (IPSec) | Private, dedicated circuit | Unified hub for VPN/ExpressRoute |
| Speed | Up to 10 Gbps (Gateway SKU) | 50 Mbps – 100 Gbps | Scalable to 20 Gbps per hub |
| Latency | Variable (internet-dependent) | Predictable (dedicated path) | Optimized via Azure backbone |
| Use Cases | Cost-effective, small-scale | Mission-critical, high-throughput | Global enterprise networks |
| Redundancy | Active-active VPN gateways | Dual circuits (geo-redundant) | Built-in HA |

---

## Architectural Scenarios:

* Basic Hybrid Setup (VPN Gateway)

  \[On-Premises Firewall\]  

  | IPSec VPN over internet 

  \[Azure VPN Gateway\] → \[Hub VNet\] ↔ \[Spoke VNets (App/DB)\]  

  Ideal for small businesses or temporary workloads.

* Enterprise Hybrid (ExpressRoute)

  \[On-Premises\] → \[ExpressRoute Circuit\] → \[Azure ER Gateway\] → \[Hub VNet\]- \[Spoke VNets\]

  Supports high-bandwidth workloads (e.g., SAP, SQL Server).

* Global Hybrid (Virtual WAN)  
    
  \[Branch Offices\] → \[SD-WAN/VPN\]    
                     ↓    
                 \[Azure Virtual WAN Hub\] ↔ \[VNets, ExpressRoute, Firewall\]    
  Centralized policy management for global enterprises.

  ---

**Security Considerations:**

* Encryption  
  VPN Gateway uses IPSec/IKEv2; ExpressRoute traffic is private but can be encrypted (e.g., MACsec).  
* Network Segmentation  
  Use Network Security Groups (NSGs) and Azure Firewall to isolate traffic between on-premises and cloud.  
* Zero Trust  
  Enforce Azure AD authentication for P2S VPNs and Just-In-Time (JIT) VM access.


**Monitoring & Management:**

* Azure Monitor: Track VPN/ExpressRoute performance (e.g., tunnel bandwidth, BGP routes).  
* Network Watcher: Diagnose connectivity issues with VPN Troubleshoot and Connection Monitor.  
* ExpressRoute Direct: Monitor circuit health and metrics (e.g., dropped packets, uptime).

**Use Cases:**

* Cloud Migration: Lift-and-shift workloads while maintaining on-premises dependencies (e.g., legacy databases).  
* Disaster Recovery: Replicate on-premises VMs to Azure with Azure Site Recovery (ASR).  
* Hybrid Applications: Run frontend APIs in Azure with backend systems on-premises.

**Best Practices:**

* Redundancy: Deploy dual VPN tunnels or ExpressRoute circuits across peering locations.  
* Performance Tuning: Use ExpressRoute FastPath for bypassing the gateway in data-heavy flows.  
* Cost Optimization: Combine ExpressRoute with VPN for failover (e.g., "ExpressRoute \+ VPN backup").  
* Compliance: Ensure data residency with Azure regions and Private Link.

  

