Azure Learn Practical:

1) Basics of Cloud Computing

a) What is Cloud ?
- It's like having a powerful computer somewhere out there on the web that you can use for tasks without needing to own or physically manage the hardware. This allows users to access data and applications from anywhere with an internet connection.

b) What is Cloud Computing ?
- Cloud computing is a technology model that involves the delivery of computing services over the internet. Instead of owning and maintaining physical servers and infrastructure, users can access and use computing resources, applications, and storage provided by either third-party service providers (public cloud) or their own organization (private cloud) through the internet. 

- Public Cloud = Shared digital space for everyone.
Who Uses It: Everyone, like individuals, businesses, and organizations.
What It's Like: Imagine a giant, shared computer space on the internet. It's like using apps, storing files, or doing tasks on the internet that anyone can access.
Example: Think of Google Drive or Amazon Web Services (AWS).

- Private Cloud = Your own exclusive digital space.
Who Uses It: One specific organization or business.
What It's Like: Picture having your own personal, private computer space. It's like a digital clubhouse where only you and your team have access. Others can't just drop in.
Example: A company using its own server for all its digital needs.

- Hybrid Cloud = Using both your private space and the shared online space when needed.
Who Uses It: A mix of everyone, depending on needs.
What It's Like: It's like having your private computer space, but sometimes you use the shared internet space too.
Example: A business storing sensitive data in its private space but using the public cloud for extra storage or specific tasks.

2) Regions and Availability Zones in Azure

a) Regions in Azure
b) Availability Zones in Azure

3) IaaS vs PaaS vs SaaS models in Azure

- Infrastructure as a Service (IaaS) =  IaaS offerings include virtual machines, storage, and networking components. Users have more control over the infrastructure but are responsible for managing and maintaining the operating system, middleware, and applications.
- Platform as a Service (PaaS) = PaaS is a cloud computing model that provides a platform allowing customers to develop, run, and manage applications without dealing with the complexity of underlying infrastructure. In Azure, PaaS offerings include Azure App Service, Azure SQL Database, and Azure Functions.
- Software as a Service (SaaS) = SaaS is a cloud computing model that delivers software applications over the internet. Users can access the software through a web browser without the need for installation or maintenance. In Azure, SaaS offerings include Microsoft 365, Dynamics 365, and many third-party applications.

4) Azure Resources, Resource Groups, ARM manager

- Azure Resources = Azure resources are the building blocks of your cloud infrastructure in Microsoft Azure. These resources can be virtual machines, databases, storage accounts, or any other service offered by Azure. Each resource is a manageable item in Azure, and they are provisioned and managed individually.
- Resource Groups = A Resource Group in Azure is a logical container for resources that share the same lifecycle, permissions, and policies. It helps you organize and manage related Azure resources efficiently. Resources within a group can be deployed, updated, and deleted together as a single management unit. (Lifecycle Management, Resource Organization & Role-Based Access Control (RBAC))
- Azure Resource Manager (ARM) = Azure Resource Manager (ARM) is the deployment and management service for Azure. It provides a consistent management layer that enables you to deploy resources with declarative templates. ARM templates describe the resources you need and their configurations, allowing you to deploy and update resources in a predictable manner. (Template-Based Deployment, Dependency Management, Rollback and Roll-forward & Tagging and Categorization)

5) Components of Virtualization

- Hypervisor (Virtual Machine Monitor):
The hypervisor is a crucial component of virtualization. It sits between the hardware and the operating systems, managing and allocating resources to virtual machines (VMs).
There are two types of hypervisors: Type 1 (bare-metal) runs directly on the hardware, while Type 2 (hosted) runs on top of an existing operating system.

- Virtual Machines (VMs):
VMs are the instances created by the hypervisor. Each VM operates as an independent computer with its own virtualized hardware, including CPU, memory, storage, and network interfaces.
Multiple VMs can run on a single physical server, allowing for efficient resource utilization.

6) create a VM and deploy Jenkins in the VM.
- create a VM with basic setup using ssh key authentication
- ssh -i <vm_key_file>.pem <username>@<public-IP>  // Example {ssh -i first-vm_key.pem vikas9821@20.189.120.89} , {chmod 600 first-vm_key.pem, //only first time}
- steps for jenkins install -> https://chatgpt.com/share/dc1baeac-13b2-40c1-b84b-d39c19e26917
// sudo apt update
// sudo apt install openjdk-11-jdk -y
// java -version
// curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
// sudo apt update
// sudo apt install jenkins -y
// systemctl list-units --type=service | grep jenkins
// sudo systemctl start jenkins, sudo systemctl enable jenkins, sudo systemctl status jenkins
// ps -ef | grep jenkins //ports

- every app installed in the server has some IP/PORT to access so for jenkins by default it uses port 8080 {ps -ef | grep jenkins, // used to check the jenkins running}
- http://20.189.120.89:8080/ // it won't work because by defualt the incoming traffic to this server is blocked by azure when its created, you need to manually open them to access.
- VM -> Network -> Network Settings -> inbound port rules -> add port -> fill and submit. // understand about ssh port open because that is also a call.
- Restart the page if it opens, then *** Congrats *** you have deployed a VM and app opened the network. 

Note: VMSS short intro for scalling the VM's

7) Azure Network (PART-01)
- Virtual Network (Vnet) = A Virtual Network (VNet) in Azure is a logically isolated network that securely connects Azure resources and extends on-premises networks. Key features include:
Isolation: VNets provide isolation at the network level for segmenting resources and controlling traffic.
Subnetting: Divide a VNet into subnets for resource organization and traffic control.
Address Space: VNets have an address space defined using CIDR notation, determining the IP address range.

- Subnets, CIDR
Subnets: Subnets are subdivisions of a Virtual Network, allowing for better organization and traffic management.
CIDR (Classless Inter-Domain Routing): CIDR notation represents IP addresses and their routing prefix, specifying the range of IP addresses for a network.

- Network Security Groups (NSGs)
NSGs are fundamental for Azure's network security, allowing filtering of inbound and outbound traffic. Key aspects include:
Rules: NSGs define allowed or denied traffic based on source, destination, port, and protocol.
Default Rules: NSGs have default rules for controlling traffic within the Virtual Network and between subnets.
Association: NSGs can be associated with subnets or individual network interfaces.

- Application Security Groups (ASGs)
ASGs group Azure virtual machines based on application requirements, simplifying network security:
Simplification: ASGs allow defining rules based on application roles instead of individual IP addresses.
Dynamic Membership: ASGs support dynamic membership based on tags or other attributes.
Rule Association: Security rules can be associated with ASGs for intuitive and scalable network security management.

- Routes and Route Tables
Routes: Routes dictate how network traffic is directed, specifying the destination and next hop.
Route Tables: Route Tables are collections of routes associated with subnets, enabling custom routing rules.

8) Azure Network (PART-02)
Example -> gated community with 4 blocks.
a) secure everything full community with gate gaurd and each gaurd for each block.
b) guest came to enter the property, main gate and block gate and flow to reach the flat in the block.

- Azure App Gateway & WAF
Azure Application Gateway = is a web traffic load balancer that enables you to manage and route traffic to your web applications. Web Application Firewall (WAF) provides protection against web vulnerabilities. Key features include:

Load Balancing: Distributes incoming traffic across multiple servers to ensure no single server is overwhelmed.
SSL Termination: Offloads SSL processing, improving the efficiency of web servers.
Web Application Firewall (WAF): Protects web applications from common web vulnerabilities and exploits.

- Azure Load Balancer
Azure Load Balancer distributes incoming network traffic across multiple servers to ensure no single server is overwhelmed. Key features include:

Load Balancing Algorithms: Supports different algorithms for distributing traffic, such as round-robin and least connections.
Availability Sets: Works seamlessly with availability sets to ensure high availability.
Inbound and Outbound Traffic: Balances both inbound and outbound traffic.

- Azure DNS
Azure DNS is a scalable and secure domain hosting service. It provides name resolution using the Microsoft Azure infrastructure. Key features include:

Domain Hosting: Hosts domain names and provides name resolution within Azure.
Integration with Azure Services: Easily integrates with other Azure services like App Service and Traffic Manager.
Global Availability: Provides low-latency responses globally.

- Azure Firewall
Azure Firewall is a managed, cloud-based network security service that protects your Azure Virtual Network resources. Key features include:

Stateful Firewall: Allows or denies traffic based on rules and supports stateful inspection.
Application FQDN Filtering: Filters traffic based on fully qualified domain names.
Threat Intelligence Integration: Integrates with threat intelligence feeds for enhanced security.

- Virtual Network Peering and VNet Gateway
Virtual Network Peering = Virtual Network Peering allows connecting Azure Virtual Networks directly, enabling resources in one VNet to communicate with resources in another. Key features include:

Global VNet Peering: Peering can be established across regions.
Transitive Routing: Traffic between peered VNets flows directly, improving performance.

- VNet Gateway = VNet Gateway enables secure communication between on-premises networks and Azure Virtual Networks. Key features include:

Site-to-Site VPN: Connects on-premises networks to Azure over an encrypted VPN tunnel.
Point-to-Site VPN: Enables secure remote access to Azure resources.

- VPN Gateway
Azure VPN Gateway provides secure, site-to-site connectivity between your on-premises network and Azure. Key features include:

IPsec/IKE VPN Protocols: Ensures secure communication over the Internet.
High Availability: Supports active-active and active-passive configurations for high availability.
BGP Support: Allows dynamic routing between your on-premises network and Azure.

9) Pratical understanding of Azure nerworking.
- Steps
- VM will be deployed in a private subnet and we only have private IP and we connect bastion to use VM.
// Create RG -> Create Vnet -> security azure bastion(used to access) and azure firewall tier basic and new policy -> IP address info default -> Create
// Create VM -> networking select vnet, subnet = default, public IP = none (you want the VM to be bhind the subnet and private) -> select (Delete NIC when VM is deleted)
- go to resource see for the public IP ? its not available.. why ? (hint = ***tion)
// vm -> connect -> bastion -> deploy bastion (5min) -> Auth Type SSH pvt key from local -> usr name -> pem file upload.
- bastion info in the portal and IAM.
- inside bastion CLI cmd's
// sudo su -   (changing user to the root user)
// sudo apt update
// sudo apt upgrade
// apt-get install nginx -y 
// sudo systemctl start nginx
// sudo vim /var/www/html/index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo Page</title>
</head>
<body>
    <h1> I Learnt how networking works in Azure today</h1>
</body>
</html> 

// sudo systemctl restart nginx

- go to firewall and make give access using IP and PORT
- Firewall policy -> settings -> DNAT rules -> add rule collection -> name -> rule type = DNAT -> Priority = 100 (lowest is high P1) -> ADD (8 min)
- add rule select rule collection grp and sub collection -> name -> source IP = (my IP) -> destination IP = FW IP -> protocol = TCP -> Destionation ports (firewall destination port) = 4000(can be any) -> Translated Type select = IP address -> Translated Address = (VM private IP) -> Translated Port = 8080 