# FortiGate-MultiZone-Network-Graduation-Project-Task1
Task 1 | Enterprise Multi-Zone Network Architecture &amp; FortiGate Firewall Security Lab (GNS3 &amp; VMware Workstation). Implemented Granular Access Policies, Static Routing, VIP/Port Forwarding, and Secure DMZ Services Reachability.
# FortiGate Multi-Zone Network: Graduation Project (Task 1)

A three-zone network (Internal / DMZ / External) secured by a **FortiGate 7.4.12** firewall, built and tested in **GNS3** and **VMware Workstation**.

The task covers per-host access policies, outbound NAT for the DMZ servers and one internal client, and publishing the internal web server to the external zone through a **Virtual IP**.

---

## Table of Contents
1. [Topology](#1-topology)
2. [Requirements](#2-requirements)
3. [Configuration](#3-configuration)
4. [Verification](#4-verification)
5. [Tools](#5-tools)

---

## 1. Topology

![Topology](<Screenshots Task 1/Topology.png>)

| Zone | Interface | Subnet | Hosts |
|---|---|---|---|
| External | port1 | 192.168.1.0/24 | Firewall external IP: 192.168.1.2 |
| DMZ | port2 | 192.168.2.0/24 | DNS (192.168.2.2), Web (192.168.2.10), FTP (192.168.2.20), File Server (192.168.2.30) |
| Internal | port3 | 172.16.10.0/24 | PC1, PC2 |

---

## 2. Requirements

| Source | Allowed destinations |
|---|---|
| **PC1** | Web server, File server, DNS server (no internet access) |
| **PC2** | FTP server, File server, DNS server, and the internet |
| **DMZ servers** (Web, DNS, FTP, File) | External zone / internet |
| **External clients** (inside the permitted address range) | Web server page, via the firewall's external IP |

Everything else is denied by the implicit deny rule.

---

## 3. Configuration

### 3.1 Interfaces

![Interfaces](<Screenshots Task 1/Network (Interfaces).png>)

### 3.2 Static default route

Default route `0.0.0.0/0` via `192.168.1.1` on port1.

![Static Route](<Screenshots Task 1/Static Route.png>)

### 3.3 Firewall policies

| # | Policy | Direction | Source | Destination | NAT |
|---|---|---|---|---|---|
| 1 | DMZ-to-External | port2 → port1 | DMZ servers | all | Enabled |
| 2 | External-to-Web | port1 → port2 | Team (permitted external range) | External-to-Web (VIP) | Disabled |
| 3 | PC1-to-Web-and-File-and-DNS | port3 → port2 | PC1 | Web, File, DNS servers | Disabled |
| 4 | PC2-to-FTP-and-File-and-DNS | port3 → port2 | PC2 | FTP, File, DNS servers | Disabled |
| 5 | PC2-to-External | port3 → port1 | PC2 | all | Enabled |
| – | implicit_deny | any | all | all | Deny |

![Policies Part 1](<Screenshots Task 1/Policies Part 1.png>)

![Policies Part 2](<Screenshots Task 1/Policies Part 2.png>)

### 3.4 Virtual IP (web publishing)

| Name | Interface | Mapped from | Mapped to |
|---|---|---|---|
| External-to-Web | port1 | 192.168.1.2 (TCP/80) | 192.168.2.10 (TCP/80) |

![Virtual IP](<Screenshots Task 1/Virtual IP (External to Web Server).png>)

---

## 4. Verification

### 4.1 PC1 (Web, File, DNS allowed; internet blocked)

**Reachability of the DNS and Web servers**

![PC1 ping DNS and Web](<Screenshots Task 1/PC1 Ping on DNS and Web.png>)

**DNS name resolution**

![PC1 DNS](<Screenshots Task 1/PC1 Request Services from DNS.png>)

**Web server access**

![PC1 Web](<Screenshots Task 1/PC1 Request Services from Web.png>)

**File server: reachability, share access, and file content**

![PC1 ping File Server](<Screenshots Task 1/PC1 Ping on File Server.png>)

![PC1 File Server share](<Screenshots Task 1/PC1 Request Services from File Server (1).png>)

![PC1 File Server file](<Screenshots Task 1/PC1 Request Services from File Server (2).png>)

**Internet access (blocked as required)**

![PC1 blocked from internet](<Screenshots Task 1/PC1 Ping on External (Block).png>)

### 4.2 PC2 (FTP, File, DNS, and internet allowed)

**Reachability of the DNS and File servers**

![PC2 ping DNS and File](<Screenshots Task 1/PC2 Ping on DNS and File Server.png>)

**DNS name resolution**

![PC2 DNS](<Screenshots Task 1/PC2 Request Services from DNS Server.png>)

**File server: share access and file content**

![PC2 File Server share](<Screenshots Task 1/PC2 Request Services from File Server (1).png>)

![PC2 File Server file](<Screenshots Task 1/PC2 Request Services from File Server (2).png>)

**FTP server: reachability, login, and file listing**

![PC2 ping FTP](<Screenshots Task 1/PC2 Ping on FTP Server.png>)

![PC2 FTP login](<Screenshots Task 1/PC2 log in FTP Server.png>)

![PC2 FTP files](<Screenshots Task 1/PC2 Request Services from FTP Server.png>)

**Internet access**

![PC2 to External](<Screenshots Task 1/PC2 to External.png>)

### 4.3 DMZ servers → External zone

| Server | Result |
|---|---|
| DNS | ![DNS to External](<Screenshots Task 1/DNS to External.png>) |
| Web | ![Web to External](<Screenshots Task 1/Web Server to External.png>) |
| FTP | ![FTP to External](<Screenshots Task 1/FTP Server to External.png>) |
| File Server | ![File Server to External](<Screenshots Task 1/File Sharing Server to External.png>) |

### 4.4 External zone → Web server (through the Virtual IP)

An external client browsing to the firewall's external IP (`http://192.168.1.2`) receives the web server's page. The Virtual IP hit counter shows 70 hits.

![External to Web Server](<Screenshots Task 1/External to Web Server.png>)

**External connectivity checks**

| Target | Result |
|---|---|
| Firewall port1 (192.168.1.2) | ![Ping my port1](<Screenshots Task 1/Ping from my PC on my Port 1.png>) |
| Second FortiGate port1 on the same external segment (192.168.1.3) | ![Ping second port1](<Screenshots Task 1/Ping from my PC on my Bro's Port 1.png>) |

### 4.5 Summary

| Test | Expected | Result |
|---|---|---|
| PC1 → Web, File, DNS | Allowed | Pass |
| PC1 → Internet | Blocked | Pass |
| PC2 → FTP, File, DNS | Allowed | Pass |
| PC2 → Internet | Allowed | Pass |
| DMZ servers → Internet | Allowed | Pass |
| External → Web page via VIP | Allowed | Pass |
| Any other traffic | Denied | Pass (implicit deny) |

---

## 5. Tools

- FortiGate VM 7.4.12 (KVM)
- GNS3 2.2.52
- VMware Workstation
- Windows Server 2019 (DMZ servers)
- Windows 10 (clients)
