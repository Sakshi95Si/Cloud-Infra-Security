# Azure Bastion
---

Azure Bastion is a fully managed service that provides secure and seamless Remote Desktop Protocol (RDP) and Secure Shell (SSH) access to Azure Virtual Machines (VMs) directly through the Azure portal. It eliminates the need for public IP addresses on VMs or complex VPN/jump host setups, enhancing security and simplifying remote access management.

## Key Features:

* Fully Managed Service: No deployment or maintenance of additional infrastructure (e.g., jump boxes).  
* Browser-Based Access: Connect to VMs directly from the Azure portal using HTTPS (port 443).  
* No Public IPs Required: VMs remain private, reducing exposure to internet threats.  
* SSL/TLS Encryption: All sessions are encrypted end-to-end using TLS 1.2.  
* Integration with Azure AD: Leverage role-based access control (RBAC) and multi-factor authentication (MFA).  
* Cross-Platform Support: Access Windows (RDP) and Linux (SSH) VMs from any device with a browser.

**How It Works:**

* User Initiates Connection: From the Azure portal, select a VM and choose Bastion as the connection method.  
* Secure Tunnel Creation: Azure Bastion establishes a secure TLS tunnel between the user’s browser and the target VM.  
* Private IP Connectivity: Bastion connects to the VM via its private IP address, ensuring traffic stays within Azure’s network.  
* Session Handling: RDP/SSH sessions are proxied through Bastion, with no direct exposure of the VM to the internet.

**Deployment Requirements:**

1. Virtual Network (VNet): Bastion must be deployed in the same VNet as the target VMs.  
2. Dedicated Subnet: A subnet named AzureBastionSubnet (minimum size /27) is required.  
3. Public IP Address: A public IP is assigned to the Bastion host (managed by Azure).  
4. Permissions: Users need Reader access to the VM and Contributor access to the Bastion resource.

**Use Cases:**

1. Secure Admin Access: Access VMs in restricted networks (e.g., finance, healthcare) without public IPs.  
2. Compliance: Meet regulatory requirements (e.g., GDPR, HIPAA) by minimizing public exposure.  
3. Hybrid Environments: Simplify access to VMs in Azure from on-premises networks via ExpressRoute/VPN.  
4. Third-Party Access: Securely grant contractors temporary access without VPNs.

**Security:**

1. Zero Public Exposure: VMs are accessed via private IPs only.  
2. Network Security Groups (NSGs): Restrict access to the Bastion subnet.  
3. Audit Logs: Track connections via Azure Monitor and Activity Logs.  
4. Azure AD Integration: Enforce MFA and RBAC policies.

**Pricing:**  
Cost Model:

1. Hourly Pricing: Based on Bastion deployment time (\~$0.19/hour for Basic tier).  
2. Data Transfer: Outbound data costs (\~$0.02/GB).  
3. No VM Licensing Costs: Only Bastion resource usage is billed.

**Setup Steps:**

1. Create the Bastion Subnet: In your VNet, add a subnet named AzureBastionSubnet (e.g., 10.0.1.0/27).  
2. Deploy Azure Bastion:  
* In the Azure portal, navigate to Bastion → Create.  
* Select the VNet, subnet, and assign a public IP.  
3. Connect to a VM: Select the VM in the portal → Connect → Bastion → Enter credentials.

**Limitations:**

1. Subnet Size: The dedicated subnet cannot be smaller than /27.  
2. Concurrent Sessions: Basic SKU supports \~25 concurrent sessions; Premium SKU offers higher limits.  
3. Protocol Support: RDP/SSH only (no VNC or custom protocols).  
4. Regional Deployment: Bastion is region-specific (deploy in the same region as VMs).

**Best Practices:**

1. Combine with Just-in-Time (JIT) Access: Temporarily enable VM access for added security.  
2. Monitor Usage: Use Azure Monitor to track Bastion connections and data usage.  
3. Deploy in High-Availability Zones: Use Premium SKU for zone-redundant deployments.  
4. Restrict Access: Apply NSGs to limit Bastion subnet traffic to trusted IP ranges.

