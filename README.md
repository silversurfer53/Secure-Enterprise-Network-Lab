# Secure Multi-VLAN Enterprise Infrastructure
**Project Owner:** Paige  
**Target Path:** CCNP Cybersecurity & Security+ Certification  
**Environment:** Cisco Packet Tracer

## 🚀 Project Overview
This project demonstrates the implementation of a secure, segmented enterprise network. The design focuses on high-speed connectivity between departments while enforcing strict security policies to protect sensitive data.



## 🏗️ Network Architecture
* **Core Layer:** Cisco 3650 Multilayer Switch (Handles Inter-VLAN routing and DHCP).
* **Access Layer:** Cisco 2960 Switch (Handles end-device connectivity and port security).
* **Trunking:** High-speed Gigabit (Gi0/1) uplink using IEEE 802.1Q encapsulation.

## 🛡️ Security Features Implemented
* **Infrastructure Hardening:** Disabled Telnet; enforced **SSHv2** with 2048-bit RSA keys.
* **Network Segmentation:** Isolated Engineering, HR, and Guest traffic using **VLANs**.
* **Access Control:** Created **Extended ACLs** to prevent Guest VLAN (30) from reaching Engineering (10).
* **Layer 2 Defense:** Implemented **Sticky Port Security** on access ports to prevent unauthorized MAC addresses from joining the network.
* **Attack Surface Reduction:** Manually disabled all unused physical ports.

## ⚙️ Technical Configuration Details

### 1. Management Plane
* Hostname: `Paige-Core-SW`
* Encrypted privileged access via `enable secret`.
* Global password encryption enabled to prevent credential exposure.

### 2. Layer 3 & DHCP
* **Inter-VLAN Routing:** Enabled `ip routing` with Switched Virtual Interfaces (SVIs) as default gateways.
* **Automated Addressing:** Configured DHCP pools for each department with excluded addresses for gateway protection.

### 3. Port Mapping
| Device | Interface | Role | VLAN |
| :--- | :--- | :--- | :--- |
| **Access-SW** | Gi0/1 | Trunk Uplink | All |
| **Access-SW** | Fa0/1 | HR PC | 20 |
| **Access-SW** | Fa0/2 | Engineering PC | 10 |
| **Access-SW** | Fa0/5-24 | Unused | Shutdown |

## 🧪 Verification Steps
The following commands were used to validate the build:
1.  `show interfaces trunk` - Confirmed the Gigabit link is active and carrying all tags.
2.  `show ip interface brief` - Verified all SVIs are "Up/Up".
3.  `show ip dhcp binding` - Confirmed PCs successfully leased 192.168.x.x addresses.
4.  `ping` - Verified that Engineering can reach the Gateway but Guests are blocked by the ACL.

---
*This lab serves as a foundational project for my cybersecurity portfolio, documenting the integration of networking fundamentals with modern security best practices.*