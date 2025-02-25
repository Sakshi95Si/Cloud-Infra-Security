# Azure Traffic Manager
---

Azure Traffic Manager is a DNS-based global traffic load balancer that distributes user requests across multiple Azure or external endpoints (e.g., web apps, VMs, cloud services) to optimize performance, availability, and reliability. It operates at the DNS layer (Layer 4), directing clients to the optimal endpoint based on configurable routing methods, health checks, and geographic rules.

## Key Features:

* Global Load Balancing: Distribute traffic across Azure regions or hybrid environments.  
* Multiple Routing Methods: Choose how traffic is routed (e.g., performance, priority, geography).  
* Health Monitoring: Continuously check endpoint health via HTTP/HTTPS probes.  
* Automatic Failover: Redirect traffic if an endpoint fails.  
* DNS-Based: No data traffic passes through Traffic Manager—only DNS resolution.  
* Hybrid Support: Works with Azure and non-Azure (on-premises/third-party cloud) endpoints.

**How It Works:**

* DNS Resolution: When a user queries your domain (e.g., app.contoso.com), Traffic Manager returns the IP of the optimal endpoint based on the configured routing method.  
  Example: A user in Europe might resolve to an endpoint in West Europe, while a user in Asia resolves to Southeast Asia.  
    
* Health Checks: Traffic Manager sends periodic HTTP/HTTPS probes to endpoints.  
  If an endpoint is unhealthy, the Traffic Manager stops directing traffic to it.  
    
* Endpoint Prioritization: Use Priority routing to define backup endpoints (e.g., primary region → secondary region).

**Components:**

* Profile: A container for settings (routing method, TTL, monitoring).  
* Endpoints: Resources to which Traffic Manager directs traffic. Types include:  
1. Azure Endpoints: Web Apps, VMs, Cloud Services.  
2. External Endpoints: On-premises servers or services in other clouds.  
3. Nested Endpoints: Child Traffic Manager profiles for complex routing.

**Traffic Routing Methods:**

Choose the method that aligns with your goals:

| Method | Use Case |
| :---- | :---- |
| Performance | Direct users to the lowest-latency endpoint (e.g., nearest Azure region). |
| Priority | Failover scenarios (e.g., primary endpoint → backup endpoint). |
| Weighted | Distribute traffic proportionally (e.g., 70% to Region A, 30% to Region B). |
| Geographic | Route users based on their geographic location (e.g., EU users → Germany). |
| Multivalue | Return multiple healthy endpoints (DNS A/AAAA records) for client-side load balancing. |
| Subnet | Map specific IP ranges to endpoints (e.g., corporate office → dedicated endpoint). |

**Health Checks & Monitoring:** 

* Probe Settings:  
1. Protocol: HTTP/HTTPS (supports custom ports and paths, e.g., /health).  
2. Interval: How often to check endpoints (default: 30 seconds).  
3. Tolerated Failures: Number of failures before marking an endpoint as unhealthy.  
     
* Endpoint Status:  
1. Online: Healthy and receiving traffic.  
2. Degraded: Partially unhealthy (e.g., slow responses).  
3. Inactive: Unavailable; removed from DNS responses.

**Use Cases:**

1. Disaster Recovery: Route traffic to a secondary region if the primary region fails.  
2. Global Performance: Use Performance routing to reduce latency for global users.  
3. A/B Testing: Use Weighted routing to split traffic between app versions.  
4. Compliance: Use Geographic routing to restrict data residency (e.g., EU data stays in Europe).

**Configuration Steps:**

1. Create a Traffic Manager Profile:  
* Choose a routing method (e.g., Performance).  
* Set DNS TTL (time-to-live) to control how long clients cache DNS results.  
2. Add Endpoints: Define Azure/external endpoints and configure health probes.  
3. Set Up Monitoring: Configure HTTP/HTTPS probes and failure thresholds.  
4. Test: Use tools like nslookup or dig to verify DNS responses.

**Example Scenario:**

Goal: Host a global web app with low latency and failover.

1. Endpoints:  
* Primary: Web App in East US  
* Backup: Web App in West Europe  
2. Routing Method: Priority (East US \= 1, West Europe \= 2).  
3. Health Checks: Probe /health every 30 seconds.  
4. Result:  
* All traffic goes to the East US.  
* If East US fails, Traffic Manager redirects users to West Europe.

**Best Practices:**

1. Combine with Azure Front Door: Use Front Door for Layer 7 features (SSL offloading, WAF) and Traffic Manager for global DNS routing.  
2. Optimize TTL: Balance between low TTL (faster failover) and high TTL (reduced DNS load).  
3. Nested Profiles: Chain profiles for advanced scenarios (e.g., Performance → Weighted).  
4. Secure Probes: Use HTTPS and authentication for health checks.

**Pricing:**

Cost Factors:

* Number of DNS queries (first 1 billion/month free, then \~$0.75/million).  
* Monitored endpoints (charged per endpoint).  
* Example: 10 endpoints \+ 5 million queries ≈ $4/month.

**Common Pitfalls:**

* DNS Caching: Clients may ignore TTL and cache old DNS entries.  
* Overlapping Geographic Rules: Conflicting regions may cause unexpected routing.  
* Misconfigured Probes: Incorrect paths/ports can mark healthy endpoints as unhealthy.

---

## Comparison with Azure Load Balancer & Front Door:

| Service | Layer | Scope | Key use case |
| :---- | :---- | :---- | :---- |
| Traffic Manager | DNS (L4) | Global | Failover, latency-based routing. |
| Azure Load Balancer | L4/L7 | Regional | Distribute traffic within a region. |
| Azure Front Door | L7 | Global | SSL termination, WAF, URL-path routing. |



