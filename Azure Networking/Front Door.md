# Azure Front Door
---

Azure Front Door (AFD) is a global, scalable content delivery network (CDN) and application acceleration service that operates at Layer 7 (HTTP/HTTPS). It enhances web application performance, reliability, and security by routing user requests to the closest or healthiest backend, enforcing security policies, and optimizing content delivery.

## Key Features:

* Global Load Balancing: Distribute traffic across Azure regions, on-premises data centers, or hybrid clouds.  
* Layer 7 Routing: URL-path, HTTP headers, or cookie-based routing (e.g., /api/\* → backend API pool).  
* Web Application Firewall (WAF): Protect against SQL injection, XSS, and other OWASP Top 10 vulnerabilities.  
* SSL/TLS Offloading: Terminate HTTPS at the edge, reducing backend server load.  
* Caching: Cache static content (e.g., images, CSS) at edge locations.  
* Health Probes: Monitor backend health and reroute traffic during failures.  
* Session Affinity: Maintain user sessions with backend via cookies.  
* DDoS Protection: Integrated with Azure DDoS Protection Standard.

**Architecture & Components:**

* Frontend: Host domain name (e.g., app.contoso.com) configured in Front Door.  
* Custom Domains: Add your own domain with SSL certificate management.  
* Backend Pools  
  Backends: Azure services (App Services, VMs, Storage) or external endpoints (on-premises, AWS).  
  Load Balancing: Weighted round-robin or latency-based routing.  
* Routing Rules  
  Conditions: Match requests based on URL path, device type, or geography.  
  Actions: Route to a backend pool, redirect, or rewrite URLs.  
* Security Policies: WAF Policies define custom or managed rules (e.g., block requests from specific IP ranges).

**How It Works:**

* User Request: A client accesses app.contoso.com.  
* DNS Resolution: The request is routed to the nearest Front Door edge location.  
* Routing Rule Evaluation:  
  Match conditions (e.g., URL path /images/\* → cache static content).  
  Apply actions (route to backend pool, redirect, or rewrite).  
* Backend Forwarding: Front Door forwards the request to the optimal backend (based on health, latency, or weights).  
* Response: The backend processes the request, and Front Door returns the response to the user.

**Use Cases:**

* Global Web Applications: Accelerate dynamic and static content for users worldwide.  
* Multi-Region High Availability: Failover to healthy regions during outages.  
* Security & Compliance: Block malicious traffic with WAF.  
* Enforce HTTPS and TLS 1.2+ encryption.  
* Blue/Green Deployments: Route traffic between app versions (e.g., 10% to v2, 90% to v1).  
* API Gateway: Route /api/\* traffic to microservices while caching static assets.

**Configuration Steps:**

1. Create a Front Door Profile: Define frontend domains (e.g., app.contoso.com).  
2. Add Backend Pools: Specify Azure or external endpoints (e.g., App Service, VM, or on-premises server).  
3. Define Routing Rules: Configure URL paths, protocols, and backend associations.  
4. Enable WAF: Apply managed or custom rulesets (e.g., block SQL injection attempts).  
5. Set Up Caching: Cache static content at edge locations (e.g., .jpg, .css).  
6. Health Probes: Monitor backend health via HTTP/HTTPS probes (e.g., /health endpoint).

**Best Practices:**

1. Enable WAF: Use managed rulesets (e.g., Microsoft\_DefaultRuleSet) for common threats.  
2. Custom Domains with HTTPS: Use Front Door-managed certificates or bring your own (BYOC).  
3. Monitor Metrics: Track latency, backend health, and WAF alerts via Azure Monitor.  
4. Caching Strategies:  
   Cache static assets with long TTL.  
   Bypass caching for dynamic content (e.g., /api/\*).  
5. Rate Limiting: Use WAF to limit request rates and prevent abuse.

**Pricing:**

1. Tier Options:  
   Standard: Basic CDN and WAF.  
   Premium: Advanced security (bot protection, custom rules).  
2. Cost Factors:  
   Data transfer out (per GB).  
   HTTP/HTTPS requests (per 10,000 requests).  
   WAF rules (per rule instance).  
   Example: 1 TB data transfer \+ 10M requests ≈ $150/month (Standard tier).  
       

**Common Pitfalls:**

* Misconfigured Routing Rules: Overlapping rules may cause unexpected routing.  
* SSL/TLS Errors: Ensure certificates are valid and domains are properly verified.  
* Caching Issues: Stale content due to incorrect cache durations or missing cache-control headers.  
* Cost Overruns: High traffic volumes or excessive WAF rules can increase costs.

**Example Scenario:**

Goal: Host a global e-commerce site with low latency, security, and failover.

* Backend Pools:  
  Primary: App Service in the East US.  
  Secondary: App Service in West Europe.  
* Routing Rules:  
  Route /static/\* to cached content.  
  Route /api/\* to backend APIs with session affinity.  
* WAF: Block SQL injection and XSS attacks.  
* Result:  
  Users in Asia connect to cached content from the nearest edge node.  
  API traffic is secured and load-balanced.  
  If the East US fails, traffic shifts to West Europe.


**Advanced Features:**

1. URL Rewrite: Modify request paths (e.g., /v2/api → /api).  
2. Custom Error Pages: Show branded 404/500 pages.  
3. Private Link Support: Connect securely to private backends (e.g., Azure VNets).



