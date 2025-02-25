# Network Watcher
---

Azure Network Watcher is a comprehensive network monitoring and diagnostics service designed to help you monitor, troubleshoot, and optimize your Azure network infrastructure. It provides tools to visualize network topologies, diagnose connectivity issues, analyze traffic, and ensure compliance with security policies.

## Key Features:

1. Monitoring & Diagnostics  
* Connection Monitor:
  Tests connectivity between Azure resources (VMs, IP addresses, URLs) and measures latency, packet loss, and network hops.
  Example: Verify if a VM can reach a database endpoint and identify latency spikes.

* VPN Diagnostics:
  Troubleshoots Azure VPN gateways and connections by analyzing logs and metrics (e.g., failed tunnels, packet drops).

* Network Performance Monitor (NPM):
  Tracks performance across hybrid networks (Azure, on-premises, or other clouds) to detect issues like latency or downtime.

2. Traffic Analysis  
* Packet Capture:
  Captures network traffic to/from a VM for deep inspection (e.g., analyzing malicious activity or protocol errors).
  Example: Capture HTTP traffic to debug an API issue.

* Flow Logs:
  Logs metadata about allowed/denied traffic through Network Security Groups (NSGs).

* Use Case: Audit security policies or investigate breaches.
  
3. Network Insights  
* Topology Tool:
  Generates a visual map of resources in a Virtual Network (VNet), showing relationships between VMs, subnets, and gateways.
  Example: Document network architecture for compliance audits.

* IP Flow Verify:
  Checks if traffic is allowed/denied by NSGs for a specific VM and port.
  Example: Diagnose why a VM can’t connect to port 80\.

* Next Hop:
  Identifies the routing path for traffic from a VM (e.g., whether traffic goes through a firewall or directly to the internet).

* Security Group View:
  Shows effective security rules applied to a VM (combining NSGs at subnet and NIC levels).

4. Diagnostic Tools  
* NSG Diagnostics:
  Analyzes NSG rules to identify misconfigurations blocking traffic.

* Latency Metrics:
  Measures round-trip time between Azure regions or on-premises locations.

   
**How to Use Azure Network Watcher:**

* Access Methods  
1. Azure Portal: Navigate to Network Watcher in the Azure portal for a GUI-based experience.  
2. CLI/PowerShell: Automate tasks like triggering packet captures or querying flow logs.  
3. REST API: Integrate diagnostics into custom applications.  
     
* Example Scenario: Troubleshooting VM Connectivity  
1. Connection Monitor: Test connectivity from VM-A to VM-B.  
2. IP Flow Verify: Check if NSG rules block port 443\.  
3. Flow Logs: Review allowed/denied traffic patterns.  
4. Packet Capture: Analyze traffic for anomalies.

**Use Cases:**

1. Troubleshooting Connectivity: Diagnose why a VM can’t reach another resource.  
2. Security Auditing: Verify NSG rules and investigate suspicious traffic.  
3. Performance Optimization: Identify latency bottlenecks in hybrid networks.  
4. Compliance: Document network topology and traffic flows for audits.  
5. VPN/ExpressRoute Health: Monitor site-to-site VPN tunnels for stability.

**Integration with Azure Services:**

1. Azure Monitor: Forward flow logs and metrics for centralized alerting and dashboards.  
2. Log Analytics: Query flow logs to create custom reports (e.g., top blocked IPs).  
3. Automation: Trigger packet captures via Azure Functions during security incidents.

**Best Practices:**

1. Enable Flow Logs: Audit traffic patterns and NSG effectiveness.  
2. Baseline Performance: Use Connection Monitor to establish normal latency/packet loss thresholds.  
3. Regular Topology Checks: Ensure network design aligns with best practices.  
4. Retention Policies: Configure storage limits for packet captures and logs to manage costs.  
5. Role-Based Access: Restrict Network Watcher access to authorized users (e.g., Network Contributor role).

**Pricing:**

1. Free Tier: Network Watcher itself is free.  
2. Costs Incurred:  
* Packet Capture: Storage costs for captured data.  
* Flow Logs: Charges for log storage and processing.  
* Network Performance Monitor: Based on monitored endpoints.

**Limitations:**

1. Regional Scope: Features like Topology and Connection Monitor are region-specific.  
2. Data Retention: Flow logs and packet captures are stored in Azure Storage, with retention limits.  
3. Complex Queries: Advanced traffic analysis may require Log Analytics expertise.

**Example Workflow:**

1. Detect high latency between regions using Connection Monitor.  
2. Use Packet Capture to analyze traffic for bottlenecks.  
3. Update NSG rules based on IP Flow Verify results.  
4. Document changes using the Topology tool.


