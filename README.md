# FortiGate-MultiZone-Network-Graduation-Project-Task1
Task 1 | Enterprise Multi-Zone Network Architecture &amp; FortiGate Firewall Security Lab (GNS3 &amp; VMware Workstation). Implemented Granular Access Policies, Static Routing, VIP/Port Forwarding, and Secure DMZ Services Reachability.
# Enterprise Network Graduation Project - Task 1

## Overview
This repository contains Task 1 of my graduation project implementation. It demonstrates a secure, multi-zone enterprise network architecture built using GNS3, VMware Workstation, and a FortiGate Firewall to manage, segment, and secure enterprise traffic.

---

## Network Topology

![Topology](./Screenshots%20Task%201/Topology.png)

---

## Security Policies & Interfaces

### 1. Network Interfaces Configuration
![Network Interfaces](./Screenshots%20Task%201/Network%20(Interfaces).png)

### 2. Static Routing Setup
![Static Route](./Screenshots%20Task%201/Static%20Route.png)

### 3. Firewall Policies (Part 1 & 2)
![Policies Part 1](./Screenshots%20Task%201/Policies%20Part%201.png)

![Policies Part 2](./Screenshots%20Task%201/Policies%20Part%202.png)

### 4. Virtual IP (VIP) & Web Server Publishing
![Virtual IP](./Screenshots%20Task%201/Virtual%20IP%20(External%20to%20Web%20Server).png)

---

## Testing & Verification

### PC1 Testing (Internal Zone Services):

* **Requesting Services from Web Server:**
  
  ![PC1 Web](./Screenshots%20Task%201/PC1%20Request%20Services%20from%20Web.png)

* **Requesting Services from DNS:**
  
  ![PC1 DNS](./Screenshots%20Task%201/PC1%20Request%20Services%20from%20DNS.png)

* **Requesting Services from File Server:**
  
  ![PC1 File 1](./Screenshots%20Task%201/PC1%20Request%20Services%20from%20File%20Server%20(1).png)
  
  ![PC1 File 2](./Screenshots%20Task%201/PC1%20Request%20Services%20from%20File%20Server%20(2).png)

* **Pings & Connectivity Tests:**
  
  ![PC1 Ping File Server](./Screenshots%20Task%201/PC1%20Ping%20on%20File%20Server.png)
  
  ![PC1 Ping DNS & Web](./Screenshots%20Task%201/PC1%20Ping%20on%20DNS%20and%20Web.png)
  
  ![PC1 Block External Ping](./Screenshots%20Task%201/PC1%20Ping%20on%20External%20(Block).png)

---

### PC2 Testing (Extended Access):

* **FTP Server Login & Services:**
  
  ![PC2 FTP Login[cite: 3]](./Screenshots%20Task%201/PC2%20log%20in%20FTP%20Server.png)
  
  ![PC2 Request FTP[cite: 3]](./Screenshots%20Task%201/PC2%20Request%20Services%20from%20FTP%20Server.png)

* **DNS & File Server Access:**
  
  ![PC2 DNS Server[cite: 3]](./Screenshots%20Task%201/PC2%20Request%20Services%20from%20DNS%20Server.png)
  
  ![PC2 File 1[cite: 3]](./Screenshots%20Task%201/PC2%20Request%20Services%20from%20File%20Server%20(1).png)
  
  ![PC2 File 2[cite: 3]](./Screenshots%20Task%201/PC2%20Request%20Services%20from%20File%20Server%20(2).png)

* **External Connectivity (Internet & Ping):**
  
  ![PC2 External[cite: 3]](./Screenshots%20Task%201/PC2%20to%20External.png)
  
  ![PC2 Ping FTP[cite: 3]](./Screenshots%20Task%201/PC2%20Ping%20on%20FTP%20Server.png)
  
  ![PC2 Ping DNS and File Server[cite: 3]](./Screenshots%20Task%201/PC2%20Ping%20on%20DNS%20and%20File%20Server.png)

---

### DMZ Servers & External Reachability:

* **DNS to External[cite: 1]:** 
  ![DNS External[cite: 1]](./Screenshots%20Task%201/DNS%20to%20External.png)

* **External to Web Server[cite: 1]:** 
  ![Ext Web[cite: 1]](./Screenshots%20Task%201/External%20to%20Web%20Server.png)

* **File Sharing Server to External[cite: 1]:** 
  ![File Ext[cite: 1]](./Screenshots%20Task%201/File%20Sharing%20Server%20to%20External.png)

* **FTP Server to External[cite: 1]:** 
  ![FTP Ext[cite: 1]](./Screenshots%20Task%201/FTP%20Server%20to%20External.png)

* **Web Server to External[cite: 1]:** 
  ![Web Ext[cite: 1]](./Screenshots%20Task%201/Web%20Server%20to%20External.png)

---

### Management & Gateway Verification:

* **Ping from PC to Port 1[cite: 3]:** 
  ![Ping Port 1[cite: 3]](./Screenshots%20Task%201/Ping%20from%20my%20PC%20on%20my%20Port%201.png)

* **Ping from PC to Bro's Port 1[cite: 3]:** 
  ![Ping Bro Port 1[cite: 3]](./Screenshots%20Task%201/Screenshots%20Task%201/Ping%20from%20my%20PC%20on%20my%20Bro%27s%20Port%201.png)
