
# Subnetting Done Right.
This project demonstrates **subnetting inside an organization** and how devices communicate **within and across subnets** using a main router and switches. Each department is assigned a separate subnet.


## Network Topology
- A **Main Router** connects all department switches.
- Each **Department (CSE, Civil, ISE, ECE) has its own switch**.
- **PCs in each department communicate through their switch**.
- The **Main Router handles inter-subnet communication**.


## IP Address Table

| Device         | Subnet            | IP Address       | Subnet Mask         | Default Gateway  |
|---------------|------------------|------------------|----------------------|------------------|
| Switch 1 (CSE) | 192.168.0.0/26   | 192.168.0.1      | 255.255.255.192      | —                |
| PC1 (CSE)     | 192.168.0.0/26   | 192.168.0.2      | 255.255.255.192      | 192.168.0.1      |
| PC2 (CSE)     | 192.168.0.0/26   | 192.168.0.10     | 255.255.255.192      | 192.168.0.1      |
| Switch 2 (Civil) | 192.168.0.64/26  | 192.168.0.65     | 255.255.255.192      | —                |
| PC3 (Civil)   | 192.168.0.64/26  | 192.168.0.66     | 255.255.255.192      | 192.168.0.65     |
| PC4 (Civil)   | 192.168.0.64/26  | 192.168.0.70     | 255.255.255.192      | 192.168.0.65     |
| Switch 3 (ISE) | 192.168.0.128/26 | 192.168.0.129    | 255.255.255.192      | —                |
| PC5 (ISE)     | 192.168.0.128/26 | 192.168.0.132    | 255.255.255.192      | 192.168.0.129    |
| PC6 (ISE)     | 192.168.0.128/26 | 192.168.0.135    | 255.255.255.192      | 192.168.0.129    |
| Switch 4 (ECE) | 192.168.0.192/26 | 192.168.0.193    | 255.255.255.192      | —                |
| PC7 (ECE)     | 192.168.0.192/26 | 192.168.0.198    | 255.255.255.192      | 192.168.0.193    |
| PC8 (ECE)     | 192.168.0.192/26 | 192.168.0.210    | 255.255.255.192      | 192.168.0.193    |

## Configuration Steps

### **Step 1: Assign IP Addresses to PCs**
1. Open each PC in **Cisco Packet Tracer**.
2. Go to `Desktop` → `IP Configuration`.
3. Assign the correct **IP address** and **Subnet Mask** from the table.
4. Set the **Default Gateway** to the router's IP for that subnet.
---
### **Step 2: Configure the Main Router**
1. Open the **Router**.
2. Assign IPs to the router interfaces:
   ```bash
   Router> enable
   Router#show ip interface brief
   
   Router# configure terminal
   
   Router(config)# interface FastEthernet0/0
   Router(config-if)# ip address 192.168.0.1 255.255.255.192
   Router(config-if)# no shutdown
   
   Router(config)# interface FastEthernet1/0
   Router(config-if)# ip address 192.168.0.65 255.255.255.192
   Router(config-if)# no shutdown
   
   Router(config)# interface FastEthernet2/0
   Router(config-if)# ip address 192.168.0.129 255.255.255.192
   Router(config-if)# no shutdown
   
   Router(config)# interface FastEthernet3/0
   Router(config-if)# ip address 192.168.0.193 255.255.255.192
   Router(config-if)# no shutdown
   ```
---
### **Step 3: Connect Switches and PCs**
- Each **department switch** should connect **all PCs in that subnet**.
- The switch **connects to the router’s respective interface**.
---

### **Step 4: Test Connectivity**
- Use **Ping Test** between PCs inside the same subnet and across subnets:
  ```bash
  ping 192.168.0.198
  ```
- Use **Simulation Mode** in Packet Tracer to observe packet flow.


## **Expected Results**
- **Devices in the same subnet can communicate** directly.
- **Inter-subnet communication works via the Main Router**.
- **Pings to different departments succeed**.
- **Network is fully functional and demonstrates proper subnetting.**

## **Conclusion**
This setup demonstrates **organizational subnetting**, **switch-based local communication**, and **router-based inter-subnet communication** in **Cisco Packet Tracer**. 
