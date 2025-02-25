# Azure DNS
---

Azure DNS is a cloud-based service provided by Microsoft Azure that lets you host and manage your domain name system (DNS) records. Think of it as a "phonebook for the internet" that translates user-friendly domain names (like www.example.com) into the numeric IP addresses (like 20.1.1.1) computers use to communicate. 

## Key Features of Azure DNS

* Global Availability: Azure DNS runs on Microsoft’s global network of servers, ensuring fast and reliable DNS resolution worldwide.  
* High Security: Built-in protection against DDoS attacks.  
* Integrates with Azure Active Directory (AAD) for role-based access control (RBAC).  
* Scalability: Automatically handles spikes in DNS queries (e.g., during traffic surges to your website).  
* Private DNS: Host DNS zones privately within your Azure Virtual Network (VNet) for internal name resolution (e.g., db-server.internal → 10.0.1.5).  
* Integration: Works seamlessly with Azure services like Virtual Machines, App Service, and Traffic Manager.

  
**How Azure DNS Works**

* Host Your Domain: Create a DNS zone in Azure (e.g., example.com).  
* Add DNS records (like A, CNAME, MX) to map names to IPs or other resources.  
* Delegate Your Domain: Point your domain registrar’s nameservers to Azure DNS (Microsoft provides the nameserver addresses).  
* Resolve Queries: When someone types www.example.com, their device queries Azure DNS, which returns the correct IP (e.g., your web server’s IP).

  
**Common Use Cases**

* Host Public Domains: Host your website’s DNS records (e.g., A records for www.example.com).  
* Private Networks: Use Azure Private DNS to resolve internal resource names (e.g., appserver.dev → 10.0.1.10) without exposing them to the internet.  
* Hybrid Cloud: Manage DNS for resources split between Azure and on-premises data centers.  
* Traffic Routing: Use alias records to point domains to Azure resources like Traffic Manager or CDN endpoints.

**Key Concepts**

* DNS Zone: A container for DNS records of a domain (e.g., example.com).  
* Record Types:  
  A: Maps a name to an IPv4 address.  
  AAAA: Maps a name to an IPv6 address.  
  CNAME: Redirects a name to another name (e.g., shop.example.com → example-store.azurewebsites.net).  
  MX: Directs email to your mail servers.

**Private DNS Zones**
Hosts DNS records for internal Azure resources (e.g., VMs, databases) within your VNet.
* Example:  
  VM name: vm01  
  Private DNS record: vm01.contoso.internal → 10.0.1.5


**Benefits:**
* No need to expose internal resources to the public internet.  
* Simplify network management with custom domain names.

**Pricing:**  
Pay based on:
* Number of DNS zones hosted.  
* Number of DNS queries (millions of queries/month).

**Common Scenarios**
* Domain Hosting: Host example.com and manage all DNS records in Azure.  
* Split-Brain DNS: Use public DNS for internet traffic and private DNS for internal VNet traffic.  
* Alias Records: Point www.example.com to an Azure Traffic Manager profile for load balancing.

**Pitfalls to Avoid**
* Misconfigured Delegation: Ensure your domain registrar points to Azure’s nameservers correctly.  
* Overlapping Public/Private Zones: Avoid naming conflicts (e.g., don’t use the same zone name for public and private DNS).

