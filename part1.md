# What is Azure Firewall?  

Azure Firewall is a fully stateful Firewall-as-a-Service (FaaS) that’s highly available and scalable. It helps secure your network by inspecting both inbound/outbound (North-South) traffic and internal (East-West) traffic.  

## Traffic Inspection Types  

### **North-South Traffic Inspection**  
Think of this as the firewall watching traffic coming into or leaving your network. For example, internet traffic flowing into an on-premises or cloud network would be considered North-South traffic inspection.  

### **East-West Traffic Inspection**  
This focuses on internal network traffic. For example, when two virtual machines (VMs) communicate within the same network.  

Azure Firewall helps enforce security policies for both types of traffic, reducing risks like unauthorized access and lateral movement of threats.  

📖 [What is Azure Firewall? | Microsoft Learn](https://learn.microsoft.com/en-us/azure/firewall/overview)  

---

## **Types of Azure Firewall**  

Azure offers three different firewall options based on security needs:  

### **Azure Firewall Basic**  
- For small and medium-sized businesses.  
- Security features: Network and application rule enforcement, threat intelligence filtering, and logging.  

### **Azure Firewall Standard**  
- For organizations needing a fully managed network firewall with security controls.  
- Supports high availability and autoscaling, including threat intelligence, domain filtering, and built-in monitoring.  

### **Azure Firewall Premium**  
- Designed for zero-trust architectures and sensitive workloads requiring deep packet inspection.  
- Adds advanced threat protection, including:  
  - TLS inspection  
  - Intrusion Detection/Prevention System (IDS/IPS)  
  - URL filtering  

---

## **How to Create an Azure Firewall**  

### **Step 1: Navigate to Resource Groups**  
1. Go to **Resource Groups** (RG) and choose the specific RG where you want to create a firewall.  
2. Click **Create** > **Search the Marketplace** (`Firewall`) > **Choose and Create**.  

### **Step 2: Configure the Firewall Subnet**  
Azure Firewall requires a subnet named **AzureFirewallSubnet**.  

1. Go to **Virtual Network (vNet1)** > **Subnets** > **Add Subnet**.  
2. Assign the **subnet address range**: `10.1.10.0`  
3. Click **Save**.
    
---
![getContent](https://github.com/GSecAwareness/Firewall/blob/main/azure%20firewall%20subnet.png)  
---
### **Step 3: Configure the Firewall**  
**Specify the following:**  
- **Name**: `myfirewalldemo`.  
- **Region**: Select your desired region.  
- **Firewall SKU**: Choose **Standard**.  
- **Create Firewall Policy**: `myfirewallpolicydemo`.  
- **Choose Virtual Network**: `vNet1`.  
- **Public IP Address**: Click **Add New** (`firewallPIP`).  
- **Enable Firewall Management NIC**: *(Uncheck if you want to disable forced tunneling and packet capture)*.  

Click **Next** > **Review and Create**.  

### **Step 4: Confirm Firewall Deployment**  
1. Go to **Resource Groups** and select your **RG**.  
2. Confirm that the **Firewall exists**.  

---
![getcontent](https://github.com/GSecAwareness/Firewall/blob/main/Firewall%20existance.png)  
---
