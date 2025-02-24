# Azure VPN Gateway

---

Azure VPN Gateway is a cloud-based service that enables secure, encrypted connectivity between Azure Virtual Networks (VNets) and on-premises networks (or other VNets) over the public internet. It acts as a virtual router, supporting site-to-site (S2S), point-to-site (P2S), and VNet-to-VNet connections using industry-standard protocols like IPSec and IKE.

**Key Components:**

1. Virtual Network Gateway

* A dedicated Azure resource deployed in a VNet’s gateway subnet (e.g., 10.0.1.0/24).  
* Requires a public IP address (static or dynamic) for internet-facing connectivity.

2. Local Network Gateway

* Represents the on-premises network’s VPN device (e.g., IP address, subnet ranges).

3. Connection

* Defines the link between the Azure VPN Gateway and the on-premises/local network gateway.

4. Gateway SKUs

* Determines performance, throughput, and features (e.g., Basic, VpnGw1, VpnGw5).

---

## Connection Types:

| Type | Use Case | Protocol |
| :---- | :---- | :---- |
| Site-to-Site(S2S) | Connect on-premises network to Azure VNet. | IPSec/IKEv1 or IKEv2 |
| Point-to-Site(P2S) | Connect individual devices (e.g., laptops) to Azure. | SSTP, OpenVPN, IKEv2 |
| Vnet-to-Vnet | Connect two Azure VNets (across regions or subscriptions). | Same as S2S (IPSec/IKE) |

---

## VPN Gateway Configurations:

1. Policy-Based vs. Route-Based

* Policy-Based: Uses static IPsec policies (e.g., source/destination IPs). Limited to Basic SKU.  
* Route-Based: Uses routing tables (BGP or static routes). Supports advanced features like active-active mode.

2. Active-Active vs. Active-Passive

* Active-Active: Two VPN gateways with unique public IPs for high availability.  
* Active-Passive: One active gateway and a standby (failover only).

## Supported Protocols & Encryption:

1. IPSec/IKE: AES-256, SHA-256, DH Group 24 (IKEv2).  
2. P2S Protocols:  
* SSTP: Port 443 (Windows-only).  
* OpenVPN: Port 443 (cross-platform).  
* IKEv2: UDP 500/4500 (macOS/iOS).

## Gateway SKUs & Performance:

| SKU | Max Throughput | Tunnels(S2S) | BGP Support | Zone Redundancy |
| :---- | :---- | :---- | :---- | :---- |
| Basic | 100 Mbps | 10 | No | No |
| VpnGw1 | 650 Mbps | 30 | Yes | Yes(AZ SKUs) |
| VpnGw5 | 1.25 Gbps | 100 | Yes | Yes |

**Note:** Higher SKUs (e.g., VpnGw4/5) support ErPAS (Equal Cost Multi-Path Routing) for higher throughput.

---

## Deployment Workflow:

1. Create a VNet with a dedicated gateway subnet (min /27).  
2. Provision a VPN Gateway with a public IP.  
3. Configure the Local Network Gateway (on-premises details).  
4. Set Up the Connection (shared key, BGP, etc.).  
5. Configure On-Premises VPN Device (e.g., Cisco ASA, FortiGate).

## Use Cases:

1. Hybrid Cloud: Securely extend on-premises data centers to Azure.  
2. Branch Office Connectivity: Connect remote offices to Azure VNets.  
3. Multi-Region VNet Peering: Link VNets across regions (e.g., VNet-to-VNet).  
4. Secure Remote Access: Allow employees to access Azure resources via P2S.

## Best Practices:

1. Choose the Right SKU: Use VpnGw2+ for production workloads requiring \>1 Gbps.  
2. Enable BGP: For dynamic routing and failover (supports route propagation).  
3. Active-Active Mode: For mission-critical HA (e.g., dual tunnels).  
4. Monitor with Azure Network Watcher: Diagnose connectivity issues (e.g., VPN Troubleshoot).  
5. Use Azure Firewall/NSGs: Restrict traffic between on-premises and Azure subnets.

## Pricing:

* Gateway Hours: Cost per hour based on SKU (e.g., VpnGw1: \~$0.10/hour).  
* Data Transfer: Charges for outbound data from Azure (ingress is free).

## Limitations:

* Basic SKU: No BGP, active-active, or zone redundancy.  
* P2S: Limited to 1,000 concurrent connections (VpnGw5).

## Example Architecture:

Hybrid S2S Setup:

\[On-Premises Network\]    
   | (IPSec over Internet)    
\[Azure VPN Gateway\] → \[Hub VNet\]    
   |    
\[Spoke VNets (App/DB)\] 

* Traffic is encrypted and routed through the VPN Gateway to Azure resources.



