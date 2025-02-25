# **Firewall Policy**  

## **Viewing Firewall Policies**  
Open the **Azure Firewall** and click on **Firewall Policy**.  
Here, you can view different policies and rules.  

📖 [Azure Firewall Policy Rule Sets | Microsoft Learn](https://learn.microsoft.com/en-us/azure/firewall/policy-rule-sets)  

The article explains that Azure Firewall Policy manages rules and settings in a structured hierarchy using Rule Collection Groups, which group related rule collections and assign them priorities. Each rule collection contains individual rules that enforce allow or deny actions. This hierarchy ensures an organized approach to processing firewall rules, enforcing priority and control over traffic. Although the default collection groups cannot be edited or modified, custom collection groups can be created for more control.  

---

## **Creating a Rule Collection**  
### **Steps to Add a Rule Collection**  
1. Navigate to **Rules > Rule Collections > Add**  
2. Specify the following details:  
   - **Name:** `fwrulecollectiondemo`  
   - **Rule Collection Type:** `Network`  
   - **Priority:** `100`  
   - **Rule Collection Action:** `Allow`  
   - **Rule Collection Group:** `DefaultNetworkRuleCollectionGroup`  

---
![getcontent](https://github.com/GSecAwareness/Firewall/blob/main/RuleCollectionDemo.png)  

---

## **Understanding Firewall Rules**  
Firewall rules protect networks by enforcing inbound and outbound rules. Inbound rules protect the network from outside threats like the internet. Outbound rules protect against malicious traffic originating from within Azure resources. There are three different rule types: DNAT, Network, and Application rules. 

### DNAT (Destination Network Address Translation) Rules  
- Redirect incoming traffic from a public IP to a private IP inside the network.  
- Used for exposing internal services like RDP or SSH to the internet.  

### Network Rules  
- Allow or deny traffic based on the network layer (L3) or transport layer (L4)
- Used to filter traffic based on IP addresses, ports, or protocols  

### Application Rules  
- Allow or deny East-West traffic based on the application layer (L7), such as Fully Qualified Domain Names (FQDNs).  
- Used for controlling access to web services, cloud apps, and blocking specific sites.  
  - Example: Allow microsoft.com and github.com while blocking facebook.com.  

---

## **Adding a Network Rule**  
### **Steps to Create a Network Rule**  
- Navigate to **Rules > Network Rules > Add a Rule**  
- Specify the following:  
   - **Rule Collection Group:** `DefaultNetworkRuleCollectionGroup`  
   - **Rule Collection:** `fwrulecollectiondemo`  
   - **Name:** `webservervm`  
   - **Source Type:** `IP Address`  
   - **Source IP Address:** `* (anywhere)`  
   - **Destination Type:** `IP Address`  
   - **Destination IP Address:** `10.2.1.20`  
   - **Protocol:** `TCP`  
   - **Port:** `443`  

---

## **Adding a DNAT Rule Collection**  
### **Steps to Create a DNAT Rule Collection**  
- Navigate to **Rules > DNAT Rules > Add a Collection**  
- Specify the following:  
   - **Name:** `dnatcollection`  
   - **Rule Collection Type:** `DNAT`  
   - **Priority:** `102`  
   - **Rule Collection Group:** `DefaultDnatCollectionGroup`  

### **Steps to Create a DNAT Rule**  
- Navigate to **Rules > DNAT Rules > Add Rule**  
- Specify the following:  
   - **Rule Collection Group:** `DefaultDnatCollectionGroup`  
   - **Rule Collection:** `dnatcollection`  
   - **Name:** `TranslateToWebServer`  
   - **Source Type:** `IP Address`  
   - **Source IP Address:** `* (any)`  
   - **Destination IP Address:** `20.232.38.43` *(Public IP from `myfirewalldemo` settings)*  
   - **Protocol:** `RCP`  
   - **Destination Ports:** `443`  
   - **Translated Type:** `IP Address`  
   - **Translated Address:** `10.2.1.20` *(Private address of the web server)*  
   - **Translated Port:** `443`  

---
![get-content](https://github.com/GSecAwareness/Firewall/blob/main/translatetowebserver.png)  

---

## **Adding an Application Rule Collection**  
### **Steps to Create an Application Rule Collection**  
- Navigate to **Rules > Applications > Add Rule Collection**  
- Specify the following:  
   - **Name:** `apprulecollection`  
   - **Rule Collection Type:** `Application`  
   - **Priority:** `105`  
   - **Rule Collection Action:** `Allow`  
   - **Rule Collection Group:** `DefaultApplicationRuleCollectionGroup`  

### **Steps to Create an Application Rule**  
- Navigate to **Rules > Applications > Add a Rule**  
- Specify the following:  
   - **Rule Collection Group:** `DefaultApplicationRuleCollectionGroup`  
   - **Rule Collection:** `apprulecollection`  
   - **Name:** `examlabpractice-webserver`  
   - **Source Type:** `IP Address`  
   - **Source IP Address:** `* (any)`  
   - **Destination Type:** `FQDN`  
   - **Target FQDN:** `examlabpractice.com`  
   - **Protocol:** `HTTPS:443`  

---
![get-content](https://github.com/GSecAwareness/Firewall/blob/main/application%20rule.png)  

---

# **Azure Firewall Manager**  

Azure Firewall Manager (AFM) is a centralized security service used to manage multiple Azure firewalls and enforce security policies across different regions and subscriptions. It provides a high-level view of firewalls and their associated resources. In addition to centralized policy management, it provides hub-and-spoke security, where a central firewall controls security for multiple connected networks. This is especially useful for businesses with multiple vNets needing shared protection, as well as for securing Azure Virtual WAN (vWAN) deployments. vWANS help businesses connect office branches and Azure resources by providing centralized routing and security in the hub-and-spoke architecture. To learn more about AFM, access the Microsoft Learn website article:  

📖 [Azure Firewall Manager | Microsoft Learn](https://learn.microsoft.com/en-us/azure/firewall-manager/overview)  

To view the current firewall policies from AFM: 
- **All Services** > **Filter Services** `Firewall Manager` > **Click to Open** > **Security** > **Azure Firewall Policies** > `myfirewallpolicydemo`




