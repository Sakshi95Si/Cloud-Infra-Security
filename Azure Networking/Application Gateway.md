# Azure Application Gateway
---

Azure Application Gateway is a Layer 7 (HTTP/HTTPS) load-balancing and web traffic management service in Azure. It acts as a reverse proxy, providing advanced routing, security, and scalability features for web applications. Unlike Azure Load Balancer (Layer 4), Application Gateway operates at the application layer, enabling intelligent traffic distribution based on URL paths, hostnames, or cookies.

## Key Features:

1. SSL/TLS Termination  
* Offloads SSL decryption/encryption at the gateway, reducing backend server load.  
* Supports end-to-end SSL (re-encrypt traffic to backend) and SSL policies (e.g., TLS 1.3, cipher suites).

2. URL Path-Based Routing  
* Directs traffic to specific backend pools based on URL paths (e.g., /api/\* to API servers, /images/\* to storage).

3. Multi-Site Hosting  
* Host multiple websites on a single gateway using hostname-based routing (e.g., app1.contoso.com and app2.contoso.com).  
    
4. Web Application Firewall (WAF)  
* Integrated WAF (via WAF SKU) protects against common threats (e.g., SQL injection, XSS, OWASP Top 10).  
    
5. Autoscaling  
* v2 SKU automatically scales based on traffic demand (supports 0–125 instances).  
    
6. Session Affinity (Cookie-Based)  
* Ensures client requests are routed to the same backend server using cookies.

7. Rewrite HTTP Headers/URLs  
* Modify request/response headers or URL paths (e.g., redirect HTTP to HTTPS).  
    
8. Redundancy & High Availability  
* Supports Availability Zones and active-active/active-passive deployments.  
    
9. Azure Kubernetes Service (AKS) Integration  
* Acts as an ingress controller for Kubernetes workloads.

---

## Core Components:

1. Frontend IP Configuration: Public (internet-facing) or private (internal) IP addresses to accept traffic.  
2. Listeners: Define how traffic is received (e.g., port 80/443, HTTP/HTTPS, hostname).  
3. Routing Rules: Bind listeners to backend pools based on conditions (e.g., URL path, HTTP headers).  
4. Backend Pools: Groups of backend servers (VMs, VMSS, AKS pods, or even external IPs).  
5. Health Probes: Monitor backend server health via HTTP/HTTPS checks (customizable intervals and paths).  
6. HTTP Settings: Configures backend protocol (HTTP/HTTPS), port, and session affinity.  
7. SSL Certificates: Upload server certificates for SSL termination or mutual authentication.

**How It Works:**

* Traffic Flow Example  
  Client → HTTPS:443 → Application Gateway →    
  (SSL Termination) → Route based on URL path →    
  Backend Pool (e.g., VMs, AKS pods)    
  The gateway decrypts traffic, inspects HTTP headers/URLs, and routes requests to the appropriate backend.  
    
* Routing Logic: Priority Order: Rules are evaluated in priority order (e.g., path-based rules first, then basic routing).  
* Example Rule: Condition: URL path starts with /api → Action: Route to backend-pool-api.

**Use Cases:**

1. Web Application Hosting: Load balance traffic across web servers, containers, or serverless apps.  
2. API Gateway: Route requests to microservices based on API endpoints.  
3. Security: Block malicious traffic with WAF and enforce HTTPS.  
4. Multi-Tenant Apps: Host multiple domains/path-based apps on a single gateway.  
5. Blue-Green Deployments: Route a percentage of traffic to new app versions for testing.

**Example Architecture:**  
\[Internet Users\]    
   ↓ HTTPS:443    
\[Application Gateway\]    
   ├── /api/\* → \[Backend Pool 1: API Servers\]    
   ├── /static/\* → \[Backend Pool 2: Blob Storage\]    
   └── /\* → \[Backend Pool 3: Web Servers\]

---

## Comparison with Other Azure Services:

| Features | App Gateway | Load Balancer | Azure Front Door |
| :---- | :---- | :---- | :---- |
| Layer | Layer 7 (HTTP/HTTPS) | Layer 4 (TCP/UDP) | Layer 7 (Global HTTP/HTTPS CDN) |
| SSl Termination | Yes | No | Yes |
| Regional/Global | Regional | Regional | Global |
| WAF integration | Yes (WAF SKU) | No | Yes (WAF policies) |
| Use Cases | Regional web apps, APIs | Non-HTTP workloads, HA ports | Global apps, CDN, DDoS protection |

**Pricing Tiers:**

* Standard v1: Fixed capacity (1–32 instances), manual scaling.  
* Standard v2/WAF v2: Autoscaling, zone redundancy, and advanced features.  
* WAF SKU: Includes OWASP rule sets, custom rules, and bot protection.

**Cost Factors:**

* Hourly gateway instance cost.  
* Data processing (per GB) for v2 SKUs.  
* WAF rules (per rule/request).

**Best Practices:**

* Use v2 SKU for autoscaling and zone redundancy.  
* Enable WAF for public-facing apps (configure custom rules as needed).  
* Centralize Certificates in Azure Key Vault for automated renewal.  
* Monitor Metrics: Track latency, backend response codes, and throughput via Azure Monitor.  
* Use Path-Based Routing to decouple microservices.  
* Enable HTTPS Redirection to enforce secure connections.

**Advanced Features:**

* Mutual Authentication (mTLS): Authenticate clients using client certificates.  
* Connection Draining: Gracefully remove backend instances during updates.  
* Custom Error Pages: Display branded error messages (e.g., 502 Bad Gateway).  
* Rewrite Rules: Modify HTTP headers (e.g., add X-Forwarded-For) or redirect URLs.

