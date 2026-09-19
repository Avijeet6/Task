# Task
# Fortune Cloud Technologies — Day 1 Practical Tasks

## AWS & Linux Networking Practical

This README documents the successful completion of all **5 Day 1 practical tasks** using Linux and AWS EC2.

---

## 🛠️ Environment Used

| Component        | Details                                |
| ---------------- | -------------------------------------- |
| Cloud Platform   | AWS                                    |
| Cloud Service    | Amazon EC2                             |
| Operating System | Amazon Linux 2023                      |
| Connection       | SSH                                    |
| Web Server       | Nginx                                  |
| Network Tools    | `ip`, `hostname`, `ping`, `curl`, `ss` |

---

# TASK 1 — Linux IP Investigation

## 🎯 Objective

To identify the Linux system's:

* IP address
* Network interface
* Default gateway
* DNS information
* Complete network configuration

## 1. Find System IP Address

### Command

```bash
hostname -I
```

### Result

The Linux system's private IP address was successfully identified.

```text
172.31.17.104
```

---

## 2. Identify Network Interface

### Command

```bash
ip -br addr
```

### Result

The active network interface was identified as:

```text
eth0
```

The interface was active and had the EC2 private IPv4 address assigned to it.

---

## 3. Find Default Gateway

### Command

```bash
ip route
```

### Result

The default route and gateway were successfully identified from the routing table.

Example format:

```text
default via <GATEWAY-IP> dev eth0
```

---

## 4. Find DNS Information

### Command

```bash
cat /etc/resolv.conf
```

### Result

The DNS configuration and nameserver information were successfully displayed.

---

## 5. Display Complete Network Configuration

### Command

```bash
ip addr
```

### Result

The complete network configuration, including the network interface, IPv4 address, subnet information and interface status, was successfully displayed.

## ✅ Task 1 Result

The Linux network configuration was successfully investigated. The IP address, network interface, default gateway, DNS configuration and complete network information were identified.

---

# TASK 2 — IPv4 Address Analysis

## 🎯 Objective

To investigate the IPv4 address assigned to the Linux machine, separate it into four octets, identify each octet value, determine whether it is private or public, and compare it with other accessible systems.

---

## 1. Identify IPv4 Address

### Command

```bash
hostname -I
```

### IPv4 Address

```text
172.31.17.104
```

---

## 2. Separate IPv4 Address into Four Octets

The IPv4 address:

```text
172.31.17.104
```

contains four octets.

| Octet     | Value |
| --------- | ----: |
| 1st Octet |   172 |
| 2nd Octet |    31 |
| 3rd Octet |    17 |
| 4th Octet |   104 |

Therefore:

```text
172 . 31 . 17 . 104
 ↑     ↑    ↑     ↑
 1st   2nd  3rd   4th
```

---

## 3. Determine Private or Public IP

The identified address is:

```text
172.31.17.104
```

This address belongs to the private IPv4 address range:

```text
172.16.0.0 – 172.31.255.255
```

Therefore:

```text
172.31.17.104 = PRIVATE IPv4 ADDRESS
```

---

## 4. Find Public IP Address

### Command

```bash
curl -4 https://checkip.amazonaws.com
```

This command was used to identify the public IPv4 address associated with the EC2 instance.

The public IP was also verified through the AWS EC2 Console.

---

## 5. Check Other Accessible Systems

Two external systems were tested for network connectivity.

### System 1

```bash
ping -c 4 8.8.8.8
```

### System 2

```bash
ping -c 4 1.1.1.1
```

Both addresses were used for IPv4 connectivity comparison.

---

## 📊 IPv4 Comparison

| System           | Address Type | IPv4            |
| ---------------- | ------------ | --------------- |
| EC2 Linux Server | Private      | `172.31.17.104` |
| System 1         | Public       | `8.8.8.8`       |
| System 2         | Public       | `1.1.1.1`       |

## ✅ Task 2 Result

The EC2 Linux machine's IPv4 address was successfully identified, divided into four octets, classified as a private IPv4 address, and compared with other accessible IPv4 systems.

---

# TASK 3 — Dynamic IP Investigation

## 🎯 Objective

To investigate dynamic IP addressing by recording the IP address before disconnecting and after reconnecting the network, then comparing both addresses.

---

## 1. Check IP Before Disconnect

### Command

```bash
hostname -I
```

### Result

```text
172.31.17.104
```

---

## 2. Check Network Interface Status

### Command

```bash
ip -br addr
```

The network interface and its current state were checked before performing the reconnect test.

---

## 3. Disconnect and Reconnect

The network connection was safely disconnected and reconnected for the practical test.

After reconnecting, the IP address was checked again.

---

## 4. Check IP After Reconnect

### Command

```bash
hostname -I
```

### Result

```text
172.31.17.104
```

---

## 5. Final Terminal Record

```text
========== BEFORE DISCONNECT ==========
IP Address: 172.31.17.104

========== AFTER RECONNECT ==========
IP Address: 172.31.17.104

IP Changed: NO
```

---

## 📊 Before vs After

| Stage             | IP Address      |
| ----------------- | --------------- |
| Before Disconnect | `172.31.17.104` |
| After Reconnect   | `172.31.17.104` |
| IP Changed        | **NO**          |

## 📝 Observation

The private IPv4 address remained the same after the network reconnect test.

The observed address was:

```text
172.31.17.104
```

This is a private IPv4 address assigned to the EC2 network interface.

## ✅ Task 3 Result

The dynamic IP investigation was successfully completed. The IP address was recorded before and after reconnecting the network, and no change was observed.

---

# TASK 4 — Cloud Linux Server & IP

## 🎯 Objective

To create an AWS EC2 Linux instance, connect to it using SSH, identify its private and public IP addresses, and compare the information shown in AWS Console with the information available inside Linux.

---

## 1. Create EC2 Instance

An AWS EC2 Linux instance was successfully created using:

```text
Operating System: Amazon Linux 2023
Service: Amazon EC2
```

The instance was configured with an appropriate security group and SSH access.

---

## 2. Connect to EC2 Using SSH

The private key was given appropriate permissions:

```bash
chmod 400 your-key.pem
```

The EC2 instance was accessed using:

```bash
ssh -i your-key.pem ec2-user@<PUBLIC-IP>
```

The SSH connection was successfully established.

---

## 3. Find Private IP from Linux

### Command

```bash
hostname -I
```

### Result

```text
172.31.17.104
```

The EC2 instance's private IPv4 address was successfully identified.

---

## 4. Verify Private IP

### Command

```bash
ip -4 addr
```

The private IPv4 address assigned to the EC2 network interface was verified.

---

## 5. Identify Network Interface

### Command

```bash
ip -br addr
```

The active network interface was identified as:

```text
eth0
```

---

## 6. Find Public IP

### Command

```bash
curl -4 https://checkip.amazonaws.com
```

The public IPv4 address was successfully obtained.

The same public IPv4 address was verified from:

**AWS Console → EC2 → Instances → Instance Details**

---

## 7. Compare AWS Console and Linux

| Information       | AWS Console           | Linux           |
| ----------------- | --------------------- | --------------- |
| Private IPv4      | EC2 Private IPv4      | `172.31.17.104` |
| Public IPv4       | EC2 Public IPv4       | `curl` result   |
| Network Interface | EC2 network interface | `eth0`          |

The IP information displayed in the AWS Console was compared with the information obtained from inside the Linux server.

## ✅ Task 4 Result

The AWS EC2 Linux server was successfully created and accessed using SSH. Both private and public IP information was identified and verified between the AWS Console and the Linux environment.

---

# TASK 5 — Cloud Network Troubleshooting

## 🎯 Objective

To troubleshoot a cloud Linux server where a service was running but could not be accessed externally.

The troubleshooting process followed a systematic approach:

```text
IP Address
    ↓
Network Interface
    ↓
Default Route
    ↓
Connectivity
    ↓
Service
    ↓
Listening Port
    ↓
Security Group
    ↓
Fix
    ↓
Final Verification
```

---

# 🔴 Problem

The Nginx web service was running on the EC2 server, but the website could not be accessed externally using the EC2 public IP address.

---

# 🔍 Troubleshooting

## 1. Check IP Address

### Command

```bash
hostname -I
```

### Result

```text
172.31.17.104
```

The server had a valid private IP address.

---

## 2. Check Network Interface

### Command

```bash
ip -br addr
```

### Result

The `eth0` network interface was active and had the private IP address assigned.

---

## 3. Check Default Route

### Command

```bash
ip route
```

### Result

The default route was present.

This confirmed that the server had a configured route for external network communication.

---

## 4. Check Network Connectivity

### Command

```bash
ping -c 4 8.8.8.8
```

### Result

Network connectivity was successfully tested.

---

# 🌐 Nginx Web Server

## 5. Install Nginx

### Command

```bash
sudo dnf install nginx -y
```

Nginx was successfully installed.

---

## 6. Start Nginx

### Command

```bash
sudo systemctl enable --now nginx
```

---

## 7. Check Nginx Service

### Command

```bash
sudo systemctl status nginx
```

### Result

```text
Active: active (running)
```

This confirmed that the Nginx service was running.

---

## 8. Check Listening Ports

### Command

```bash
sudo ss -tulpn
```

The Nginx service was found listening on:

```text
TCP Port 80
```

---

## 9. Test Web Server Locally

### Command

```bash
curl -I http://localhost
```

### Result

```text
HTTP/1.1 200 OK
```

This confirmed that Nginx was working correctly on the server itself.

---

# 🚨 Identify the Cause

The Linux server was functioning correctly:

```text
IP              → Working
Network         → Working
Default Route   → Present
Nginx           → Running
Port 80         → Listening
Local HTTP      → Working
```

The problem was therefore identified at the **AWS Security Group** level.

The EC2 Security Group did not have an inbound rule allowing HTTP traffic on:

```text
TCP Port 80
```

---

# 🛠️ Solution

An inbound HTTP rule was added to the EC2 Security Group.

```text
Type       : HTTP
Protocol   : TCP
Port       : 80
Source     : Appropriate allowed source
```

SSH port 22 was kept available for administrative access.

---

# ✅ Final Verification

After adding the HTTP/80 security rule, the Nginx web server was accessed through the EC2 public IPv4 address.

The final communication path was:

```text
Browser
   ↓
EC2 Public IPv4
   ↓
AWS Security Group
   ↓
TCP Port 80
   ↓
Nginx
   ↓
Web Page
```

## ✅ Task 5 Result

The network problem was successfully identified and resolved.

### Final Troubleshooting Summary

| Stage                 | Result                 |
| --------------------- | ---------------------- |
| IP Address            | ✅ Working              |
| Network Interface     | ✅ Working              |
| Default Route         | ✅ Working              |
| Internet Connectivity | ✅ Working              |
| Nginx Service         | ✅ Running              |
| Port 80               | ✅ Listening            |
| Local HTTP Test       | ✅ Successful           |
| Security Group        | ❌ HTTP/80 rule missing |
| Solution              | ✅ Added HTTP/80        |
| Final Website Access  | ✅ Working              |

---

# 📸 Screenshot Evidence

Screenshots were captured for the major practical steps and organized according to task number.

## Task 1

* IP address
* Network interface
* Default gateway
* DNS information
* Complete network configuration

## Task 2

* IPv4 address
* Four-octet analysis
* Private/public classification
* Connectivity to other systems

## Task 3

* Before disconnect
* After reconnect
* IP comparison
* Final `IP Changed: NO` result

## Task 4

* EC2 instance
* Successful SSH connection
* Private IP
* Public IP
* AWS Console IP information
* IP comparison

## Task 5

* Network troubleshooting
* Nginx status
* Port 80
* Local HTTP test
* Security Group configuration
* Final working web server

---

# 🧠 Key Learning Outcomes

After completing these practicals, the following concepts were practiced:

* Linux IP configuration
* IPv4 addressing
* IPv4 octets
* Private and public IP addresses
* Network interfaces
* Default gateways
* DNS configuration
* Dynamic IP behavior
* AWS EC2
* SSH
* AWS Security Groups
* TCP ports
* Nginx
* Network connectivity testing
* Listening ports
* Cloud network troubleshooting

---

# 🏁 Final Conclusion

All **5 Day 1 practical tasks** were completed successfully using Linux and AWS EC2.

The practical provided hands-on experience with Linux networking, IPv4 addressing, AWS EC2 networking, SSH connectivity, web-server deployment, security groups, and systematic cloud network troubleshooting.

**Overall Status: ✅ COMPLETED**
