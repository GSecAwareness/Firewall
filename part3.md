# Create a Route Table  

To direct traffic to the firewall, create a route table from within the resource group.  

**Steps to Create a Route Table:**  
- Navigate to **Resource Groups > vNetDemoRG > Create**.  
- Search the Marketplace for **“Route Table”**, then click to open and **Create**.  

**Specify the following:**  
- **Region:** East US  
- **Name:** `myfirewallroutetable`  
- **Propagate gateway routes:** Yes  

### **Add Routes to the Route Table**  
- Go to the resource (`myfirewallroutetable`) > **Settings** > **Routes** > **Add**.  
- Specify the following:  
   - **Route Name:** `RouteThroughFW`  
   - **Destination Type:** `IP Address`  
   - **Destination IP addresses:** `10.0.0.0/8`  
   - **Next Hop Type:** `Virtual appliance (our firewall)`  
   - **Next Hop Address:** `10.1.10.4` *(Private IP address of `myfirewalldemo`, located in the resource’s overview)*.  

---
![get-content](https://github.com/GSecAwareness/Firewall/blob/main/private%20IP%20of%20firewall.png)  

---

### **Associate the Route Table with Subnets**  
- Go to the resource (`myfirewallroutetable`) > **Settings** > **Subnets** > **Associate**.  
- Specify the following:  
   - **Virtual Network:** `vNet1 (vNetDemoRG)`  
   - **Subnet:** `Subnet1A`  
- Repeat the process for **Subnet1B**.  
- Repeat the process for the **other vNets and subnets**.  

---
![get-content](https://github.com/GSecAwareness/Firewall/blob/main/finish%20wubnet%20pic.png)  

---

### **Deleting the Firewall and Resources**  
Since running a firewall incurs costs, you may want to **delete the resources** once you're done.  

**Steps to Delete Everything Created:**  
1. Navigate to **Resource Groups**.  
2. Click on the **Resource Group**.  
3. Select **Delete Resource Group**.  

