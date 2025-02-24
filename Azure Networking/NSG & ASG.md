# Network Security Groups (NSGs)

---

NSGs act as virtual firewalls that filter network traffic to/from Azure resources (like VMs, subnets, or NICs). They enforce rules to allow or deny traffic based on:

* Source/destination IP addresses  
* Ports (e.g., HTTP on port 80\)  
* Protocols (e.g., TCP, UDP)

**Key Features:**

* Stateful filtering: Automatically allows return traffic for allowed connections (e.g., if you allow inbound HTTP, outbound responses are auto-permitted).  
* Hierarchical rules: Apply NSGs to entire subnets or individual VMs/NICs.  
* Priority-based rules: Rules are processed in numerical order (lower numbers \= higher priority).  
    
  **Example NSG Rule:**  
    
  Name: Allow-HTTP    
  Priority: 100    
  Source: Any    
  Source Port: \*    
  Destination: 10.0.1.5    
  Destination Port: 80    
  Protocol: TCP    
  Action: Allow    
  This allows HTTP traffic to a VM with IP 10.0.1.5.  
    
  **Common Use Cases:**  
    
* Block SSH/RDP access from the public internet.  
* Allow internal traffic between VMs in a subnet.  
* Restrict outbound traffic to specific IP ranges.

---

# Application Security Groups (ASGs)

ASGs let you group VMs by application role (e.g., "WebServers" or "Databases") and apply NSG rules to the group instead of individual IPs. This simplifies security management for dynamic environments.

**Key Features:**

* Role-based grouping: Assign VMs to groups like "Web", "App", or "DB".  
* Dynamic scaling: New VMs added to the group inherit existing rules.  
* Simplified rules: Replace complex IP-based rules with logical group names.  
    
  **Example ASG Rule:**  
    
  Name: Allow-Web-to-App    
  Priority: 200    
  Source: ASG-Web    
  Destination: ASG-App    
  Destination Port: 8080    
  Protocol: TCP    
  Action: Allow    
  This allows traffic from VMs in the "Web" group to VMs in the "App" group on port 8080\.


**Common Use Cases:**

* Allow communication between frontend and backend tiers (e.g., web servers → app servers).  
* Restrict database access to specific application tiers.  
* Simplify rules for auto-scaling VM fleets.

---

**How NSGs and ASGs Work Together**

* Create ASGs: Define groups like ASG-Web, ASG-App, and ASG-DB.  
* Assign VMs: Add VMs to these groups (e.g., web servers to ASG-Web).  
* Write NSG Rules: Use ASGs instead of IPs in NSG rules.

Example: "Allow ASG-Web to access ASG-App on port 8080."

---

**Key Differences**

| Feature | NSGs | ASGs |
| :---: | :---: | :---: |
| Purpose | Define traffic rules (allow/deny). | Group VMs by role for rule reuse. |
| Scope | Subnets, NICs, or VMs. | VMs only. |
| Rule flexibility | IP/port/protocol-based. | Role-based (logical groupings). |

**Best Practices**

* Use ASGs for role-based rules: Avoid hardcoding IPs in NSGs.  
* Minimize open ports: Only allow necessary traffic (e.g., block port 22 for SSH from the internet).  
* Combine with Service Tags: Use Azure’s predefined tags (e.g., Internet, AzureLoadBalancer) to simplify rules.  
* Audit NSGs: Use Azure Network Watcher to analyze effective security rules.

**Pitfalls to Avoid**

* Overly permissive rules: Avoid Source: Any for critical resources.  
* Conflicting rules: Ensure higher-priority rules don’t block necessary traffic.  
* Forgetting ASGs: Manually updating IP-based rules becomes error-prone as VMs scale.

