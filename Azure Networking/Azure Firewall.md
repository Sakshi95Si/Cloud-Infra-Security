# Azure Firewall
---

Azure Firewall is a cloud-native, managed network security service provided by Microsoft Azure. It acts as a gatekeeper for your Azure Virtual Network (VNet), controlling inbound and outbound traffic to protect your cloud resources from unauthorized access, cyber threats, and malicious activity. 

## Key Features

* Stateful Firewall:  
  Tracks active connections (like TCP/UDP sessions) to allow legitimate traffic and block suspicious activity.  
  Example: If a user connects to a web server, Azure Firewall ensures responses go back only to that user.  
    
* Application Filtering:  
  Controls access based on application protocols (e.g., HTTP, FTP, RDP) or domain names (e.g., \*.microsoft.com).  
  Example: Block social media sites but allow access to business tools like Office 365\.  
    
* Network Address Translation (NAT):  
  Hides private IPs of internal resources (e.g., databases, VMs) by translating them to a public IP when exposed to the internet.  
  Example: Redirect traffic from a public IP (e.g., 20.1.1.1:443) to a private web server (10.0.1.10:443).  
    
* Threat Intelligence:  
  Blocks traffic from known malicious IPs/domains using Microsoft’s threat intelligence feeds.  
  Example: Automatically stops ransomware or phishing attempts.  
    
* Centralized Management:  
  Create and enforce security rules across multiple Azure subscriptions and VNets from a single dashboard.

**Common Use Cases**

* Secure Internet Access: Filter outbound traffic (e.g., block risky websites).  
* Protect Internal Resources: Hide backend servers (like databases) from direct internet exposure.  
* Compliance: Enforce rules to meet regulatory requirements (e.g., PCI DSS).  
* Hybrid Networks: Secure traffic between on-premises data centers and Azure.

**Benefits:**

* Fully Managed: No hardware to maintain—Azure handles updates and scaling.  
* Integration: Works seamlessly with Azure services like VNets, Load Balancers, and Security Center.  
* High Availability: Built-in redundancy to avoid downtime.


---

# Network Address Translation

NAT (Network Address Translation) Rules in Azure Firewall are used to translate incoming traffic from a public IP address/port to a private IP address/port within your virtual network. This is commonly referred to as DNAT (Destination NAT) and is critical for securely exposing internal services (e.g., web servers, RDP/SSH access) to the internet while keeping backend resources private.

## Key Use Cases for NAT Rules

* Hosting Public Services: Expose internal web servers, APIs, or databases.  
* Remote Access: Securely allow RDP/SSH to VMs without public IPs.  
* Port Redirection: Map a public port to a different private port (e.g., public port 8080 → private port 80).

**How NAT Rules Work in Azure Firewall**

* Public IP: Traffic is sent to a public IP associated with the Azure Firewall.  
* Rule Processing: Azure Firewall evaluates the NAT rule, translates the destination IP/port, and forwards traffic to the internal resource.  
* Implicit Allow: NAT rules automatically create an associated network rule to allow the translated traffic (no need for a separate allow rule).

**Implementation Steps**  
1\. Prerequisites

* An Azure Firewall deployed in your VNet.  
* A public IP address assigned to the firewall.  
* Internal resources (e.g., VMs) with private IPs.

2\. Configure a NAT Rule

* Rule Name: Descriptive name (e.g., WebServer-DNAT).  
* Protocol: TCP/UDP.  
* Source Type: Use IP Address or Service Tag (e.g., Internet).  
* Source Addresses: Restrict to specific IP ranges (e.g., your office IP) for security.  
* Destination Addresses: The firewall’s public IP.  
* Destination Ports: Public port (e.g., 443 for HTTPS).  
* Translated Address: Private IP of the backend resource.  
* Translated Port: Internal port (e.g., 443 or 80).

3\. Configure Network Routes

* Ensure traffic to the backend resource routes through the Azure Firewall (e.g., via a User-Defined Route (UDR) in the subnet).

4\. Test Connectivity

* Use tools like curl, telnet, or a browser to verify access to the public IP/port.

**Example Scenario**: Hosting a Web Server

* Public IP: 20.1.1.1 assigned to Azure Firewall.  
* NAT Rule:Translate 20.1.1.1:443 → 10.0.1.10:443 (internal web server).  
* Network Rule (Automatically Created):Allow traffic from the Internet to 10.0.1.10:443.  
* Application Rule (Optional): Allow \*.mydomain.com for Layer 7 filtering.

**Common Pitfalls to Avoid**

* Misconfigured Routes: Ensure subnets route traffic through the firewall via UDRs.  
* Open Source IP Ranges: Never use 0.0.0.0/0 unless absolutely necessary.  
* Port Conflicts: Avoid reusing the same public port for multiple NAT rules.  
* Ensure NAT rules don’t conflict with Application/Network rules.

**Advanced: NAT Rule Collections**

* Group NAT rules into collections with shared priority. Higher priority rules are processed first.  
* Use FQDN Tags (e.g., WindowsUpdate) to simplify rule creation for known services.


