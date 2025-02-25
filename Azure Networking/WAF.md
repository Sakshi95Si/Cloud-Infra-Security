# Azure Web Application Firewall(WAF)
---

Azure Web Application Firewall (WAF) is a cloud-native service designed to protect web applications from common vulnerabilities and attacks by inspecting and filtering HTTP/HTTPS traffic. It integrates with Azure Application Gateway (for regional protection) and Azure Front Door (for global protection), offering centralized security, scalability, and ease of management.

## Key Features:

1. Protection Against OWASP Top 10 Threats: Blocks attacks like SQL injection, cross-site scripting (XSS), command injection, and HTTP request smuggling.  
2. Bot Protection: Mitigates malicious bots using managed rulesets (e.g., scraping, credential stuffing).  
3. Geo-Filtering: Restricts traffic by geographic location (e.g., block requests from specific countries).  
4. Custom Rules: Define application-specific rules (e.g., block IP ranges, regex-based URL filtering).  
5. Managed Rule Sets: Pre-configured rules managed by Microsoft (e.g., OWASP 3.2, 3.1, or 3.0).  
6. Logging & Monitoring: Integrates with Azure Monitor and Log Analytics for real-time insights.  
7. TLS/SSL Offloading: Terminates HTTPS at the edge, reducing backend server load.

**How It Works:**

1. Traffic Flow: Incoming requests pass through the WAF (deployed on Application Gateway or Front Door).  
2. Rule Evaluation: Requests are checked against managed rules (predefined) and custom rules (user-defined).  
3. Action Enforcement: Matched requests are blocked, logged, or allowed based on the configured policy.  
4. False Positive Mitigation: Use exclusion lists to ignore specific request attributes (e.g., headers, cookies).

**Deployment Options:**

1. Azure Application Gateway WAF (Regional)  
   Use Case: Protect web apps within a single Azure region.  
* Layer 7 load balancing.  
  TLS termination.URL path-based routing.  
* SKUs: WAF\_v2 (Recommended): Auto-scaling, zone redundancy, advanced rule tuning.  
  WAF\_v1: Basic features with manual scaling.

2. Azure Front Door WAF (Global)
   Use Case: Protect globally distributed apps with edge-level security.

* Global CDN integration.  
* DDoS protection.  
* Low-latency routing.

**WAF Policies:**

A WAF policy is a collection of rules and settings applied to Application Gateway or Front Door.

1. Managed Rules:  
* OWASP Core Rule Sets (CRS): Predefined rules for common vulnerabilities.  
* Microsoft Bot Manager: Blocks malicious bots.  
2. Custom Rules:   
* Match Conditions: IP address, geo-location, request headers, body content.  
* Actions: Allow, block, log, or redirect.  
3. Policy Association:  
* One policy can be linked to multiple Application Gateway or Front Door instances.

**Configuration Steps:**

1. Create a WAF Policy:   
* In the Azure portal, navigate to WAF Policy → Create.  
* Select a rule set (e.g., OWASP 3.2).  
2. Add Custom Rules (Optional):  
* Define rules like "Block requests from IP range X."  
3. Associate with Application Gateway/Front Door:  
* Link the policy during resource creation or later.  
4. Test in Detection Mode:  
* Log malicious requests without blocking them initially.  
5. Switch to Prevention Mode:  
* Block attacks after tuning rules to minimize false positives.

**Monitoring & Logging:**

1. Azure Monitor: Track metrics like blocked requests, WAF latency, and bot traffic.  
2. Log Analytics: Query detailed logs (e.g., AzureDiagnostics | where Category \== "ApplicationGatewayFirewallLog").  
3. Alerting: Set up alerts for critical events (e.g., SQL injection attempts).

**Use Cases:**

* E-Commerce Security: Block credit card skimming attacks (Magecart).  
* Compliance: Meet PCI-DSS requirements by protecting payment gateways.  
* Hybrid Apps: Secure apps spanning Azure and on-premises environments.  
* API Protection: Safeguard RESTful APIs from malicious payloads.

**Best Practices:**

* Start in Detection Mode: Identify false positives before blocking traffic.  
* Regular Updates: Use the latest OWASP CRS version (e.g., 3.2).  
* Custom Rules: Block traffic from high-risk regions or known bad IPs.  
* Exclusion Lists: Ignore benign traffic (e.g., user-agent strings for legacy systems).  
* Layered Security: Combine WAF with Azure DDoS Protection and Network Security Groups (NSGs).

**Example Scenario:**  
Goal: Protect a healthcare app storing sensitive patient data.

1. Deploy Application Gateway WAF\_v2 in prevention mode with OWASP 3.2 rules.  
2. Add Custom Rules:   
* Block traffic from non-US regions.  
* Block requests containing /admin paths unless from a trusted IP.  
3. Enable Bot Protection: Block scraping bots.  
4. Monitor Logs: Alert on SQL injection attempts.
* Result: The app is shielded from attacks while complying with HIPAA requirements.

