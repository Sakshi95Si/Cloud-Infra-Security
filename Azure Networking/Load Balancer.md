# Azure Load Balancer
---

Azure Load Balancer is a Layer 4 (Transport Layer) networking service in Azure that distributes incoming traffic across healthy backend resources (e.g., virtual machines, VM scale sets) to ensure high availability, scalability, and low-latency performance. It operates at the TCP/UDP protocol level and is a foundational component for building resilient cloud applications.

## Key Features

1. High Availability  
* Distributes traffic across multiple backend instances to prevent downtime.  
* Monitors backend health via health probes (TCP/HTTP/HTTPS) and reroutes traffic if a resource fails.  
2. Scalability  
* Handles millions of requests per second (Standard SKU).  
* Integrates with VM Scale Sets for automatic scaling.  
3. Public & Internal Load Balancing  
* Public Load Balancer: Routes internet traffic to backend resources (e.g., web servers).  
* Internal Load Balancer (ILB): Balances traffic within a Virtual Network (VNet) or on-premises networks (e.g., database tier).  
4. Port Forwarding  
* Direct specific ports to backend resources (e.g., SSH/RDP to individual VMs).  
5. Outbound Connectivity  
* Provides outbound internet access for backend resources via SNAT (Source Network Address Translation).  
6. Availability Zones (Standard SKU)  
* Zone-redundant or zonal deployments for fault tolerance.

  
**Core Components:**

* Frontend IP Configuration  
  Public or private IP address where traffic enters the load balancer.  
  Example: A public IP 20.100.100.1 for internet-facing apps.  
    
* Backend Pool  
  Group of backend resources (VMs, NICs, IP addresses) that receive traffic.  
  Example: A pool of 5 web servers hosting an application.

* Health Probes  
  Checks the health of backend instances (TCP/HTTP/HTTPS).  
  Unhealthy instances are removed from the pool until they recover.
  
* Load Balancing Rules  
  Defines how traffic is distributed.  
  Maps frontend IP/port to backend IP/port (e.g., port 80 → port 8080).  
    
* HA Ports (Standard SKU)  
  Load-balances all ports (e.g., for scenarios like Network Virtual Appliances).  
  

**Use Cases:**

* Web Traffic Distribution: Balance HTTP/HTTPS traffic across web servers.  
* Hybrid Workloads: Combine public and internal load balancing for multi-tier apps (e.g., web tier \+ database tier).  
* Disaster Recovery: Redirect traffic to a secondary region during outages.  
* Non-HTTP Services: Load-balance TCP/UDP protocols (e.g., gaming servers, VoIP).

**How It Works:**

* Traffic Flow  
  A client sends a request to the Load Balancer’s frontend IP.  
  The Load Balancer uses hashing (source IP, port, protocol) to route the request to a backend instance.  
  Health probes continuously monitor backend instances.  
* Session Persistence: Optional source IP affinity ensures a client’s requests go to the same backend instance.  
* Example Workflow  
  Client → Public IP:80 → Load Balancer → Backend Pool (VM1, VM2, VM3)   
  
---

## Comparison with Other Azure Services:

| Feature | Azure Load Balancer | Application Gateway | Traffic Manager |
| :---- | :---- | :---- | :---- |
| Layer | Layer 4(TCP/UDP) | Layer 7(HTTP/HTTPS) | DNS based(global) |
| SSL Termination | No  | Yes | Yes |
| Global or Regional | Regional | Regional | Global |
| Use cases | Non-HTTP, high perf | Web apps, SSL offload | Geo-distributed apps  |

**Pricing:**

* Basic SKU: Free (limited features, no SLA).  
* Standard SKU:  
  Charged per hour \+ data processed (ingress/egress).  
  HA Ports and Availability Zones incur additional costs.

**Best Practices:**

* Use Standard SKU for production workloads (supports HA, zones, and advanced features).  
* Enable Health Probes to avoid routing traffic to unhealthy instances.  
* Combine with NSGs to restrict traffic to/from backend pools.  
* Use HA Ports for Network Virtual Appliances (NVAs).  
* Monitor with Azure Monitor for metrics like data throughput and health probe status.

**Example Architecture:**

\[Internet Users\]    
   ↓    
\[Azure Public Load Balancer (Frontend IP: 20.100.100.1)\]    
   ↓    
\[Backend Pool: Web Servers (VM1, VM2, VM3)\]    
   ↓    
\[Internal Load Balancer\] → \[Database Tier (VM4, VM5)\] 

