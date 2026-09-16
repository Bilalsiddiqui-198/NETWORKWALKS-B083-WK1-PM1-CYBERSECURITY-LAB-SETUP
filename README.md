
# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice using VirtualBox and Kali Linux**

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000)
![VirtualBox](https://img.shields.io/badge/VirtualBox-v7.2-0070C0?style=flat-square&labelColor=000000)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000)
![Status](https://img.shields.io/badge/Status-In%20Progress-C00000?style=flat-square&labelColor=000000)

---

## 📌 Project Overview

This project documents the setup of a **virtual cybersecurity and penetration-testing lab** using VirtualBox and Kali Linux.

The goal is to build a controlled, isolated environment where network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be practiced safely and repeatedly — without touching any production or public network.

The lab runs on a private virtual network so additional target machines can be added later for hands-on, authorized testing exercises.

---

## 🎯 Objectives

- Install and configure VirtualBox as the hypervisor.
- Install/import Kali Linux as a virtual machine.
- Create a private **NAT Network** dedicated to the lab.
- Configure the Kali VM's network adapter and connectivity.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Document the complete setup process, issues, and fixes.

---

## 🛡️ Purpose of the Lab

This lab provides an isolated environment for cybersecurity learning and authorized security testing, including:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web application security testing
- Exploitation practice
- General security-tool experimentation

> ⚠️ **Important:** This lab is for systems you own or have explicit permission to test. Never use it against unauthorized systems or networks.

---

## ⚙️ Lab Configuration

| Component          | Configuration              |
|--------------------|-----------------------------|
| 🖥️ Host OS          | Windows 11                  |
| 🧠 Host RAM         | 8 GB                         |
| ⚡ Processor        | Intel Core i5/i7             |
| 🧰 Hypervisor       | VirtualBox 7.2                |
| 🐉 Guest OS         | Kali Linux 2026.2              |
| 🧠 Kali RAM         | 2048 MB                        |
| 🌐 Virtual Network  | NAT Network                    |
| 📡 Network Address  | 10.0.0.0/24                     |
| 🐧 Kali IP Address  | 10.0.0.2/24                      |
| 🚪 Default Gateway  | 10.0.0.1                          |
| 🌍 DNS Server       | 8.8.8.8                             |
| 🔮 Future VM Range  | 10.0.0.3 – 10.0.0.99                 |

---

## 📂 Repository Structure

```
NETWORKWALKS-B0XX-WK1-PM1-CYBERSECURITY-LAB-SETUP/
│
├── README.md
├── screenshots/
│   ├── nat-network.png
│   ├── kali-network-adapter.png
│   ├── kali-desktop.png
│   ├── ip-address-verification.png
│   ├── gateway-ping.png
│   ├── internet-ping.png
│   └── dns-resolution.png
```

---

# 🪜 Lab Setup Procedure

## Step 1. Install VirtualBox

Downloaded and installed VirtualBox from the official site to serve as the hypervisor for the lab.

**Tool:** VirtualBox 7.2

---

## Step 2. Create the NAT Network

Created a dedicated NAT Network inside VirtualBox so multiple VMs can talk to each other while still reaching the internet.

```
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
```

![NAT Network Settings](1-NATNETWORK.png)
![NAT Network Settings](2-NATNETWORK-VM-Setting.png)

A **NAT Network** (rather than plain NAT) was used because it lets multiple VMs on the same network communicate with one another — needed for future attacker/target VM setups — while still giving outbound internet access.

---

## Step 3. Import Kali Linux

Downloaded the official Kali Linux VirtualBox image and imported it as a new VM.

Network adapter configuration:

```
Adapter 1
Attached to:   NAT Network
Name:          NatNetwork
Adapter Type:  Intel PRO/1000 MT Desktop (82540EM)
Promiscuous Mode: Allow All
```

Allocated resources:

```
RAM: 2048 MB
```
![Kali Linux Login](3-login.png)
![Kali Linux Desktop](4-Linux_Desktop.png)
![Kali Network Adapter Settings](5-Network_settings.png)

> 💡 Note: Network adapter settings (like Adapter Type and MAC Address) are locked while the VM is running or in a saved state — power the VM off completely before editing them.

---

## Step 4. Configure the Kali Linux Network

Verified and set a consistent IP configuration inside the Kali VM.

```
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0
Gateway:      10.0.0.1
DNS:          8.8.8.8
```

![IP Address Verification](5-Network_settings.png)

A fixed IP makes it easier to document the lab and reference the Kali machine in future exercises.

---

# 🔎 Lab Verification

| Test                     | Command                       | Expected Result             | Screenshot |
|---------------------------|-------------------------------|------------------------------|------------|
| Check IP address           | `ip a`                        | Correct Kali IP shown        | `ip-address-verification.png` |
| Test gateway               | `ping -c 4 10.0.0.1`            | Successful replies           | `gateway-ping.png` |
| Test internet connectivity | `ping -c 4 8.8.8.8`              | Successful replies           | `internet-ping.png` |
| Test DNS resolution        | `nslookup google.com`             | Domain resolves               | `dns-resolution.png` |
| Verify Nmap install        | `nmap --version`                   | Nmap version displayed        | — |

![Gateway Ping Test](screenshots/gateway-ping.png)
![Internet Connectivity Test](screenshots/internet-ping.png)
![DNS Resolution Test](screenshots/dns-resolution.png)


# 🐞 Problems Encountered & Solutions

## Problem 1: Network adapter settings greyed out

While editing the Kali VM's network settings, some options (Adapter Type, MAC Address, Enable Network Adapter) appeared greyed out and couldn't be changed.

**Cause:** The VM was still running or in a saved state — VirtualBox locks these settings until the machine is fully powered off.

**Fix:**
1. Fully shut down the VM (ACPI shutdown from inside the guest, or Close → Power Off from VirtualBox Manager).
2. Reopen Settings → Network.
3. Adapter settings became editable.

## Problem 2: [Add another issue you ran into, if any]

Description of the problem...

**Fix:** Steps taken to resolve it...

---

# 📋 Known Limitations / Pending Work

- **VM Snapshot not yet taken.** A clean baseline snapshot (e.g. `Clean Kali - Network Setup`) was not created after the initial configuration. This is planned as a follow-up step before any exploitation or vulnerability-testing exercises are run on this VM, so the environment can be reliably restored if something breaks.

---

# 💡 What I Learned

### 1. NAT vs NAT Network
A NAT Network lets multiple VMs on the same virtual network talk to each other while still sharing outbound internet access — essential for a multi-machine lab.

### 2. VM Network Adapter Locking
Several network adapter settings are locked while a VM is running or saved, and only become editable once the VM is fully powered off.

### 3. Static IP Configuration
Learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS on Kali Linux.

### 4. Importance of Snapshots
Learned that a clean snapshot should ideally be taken right after the base setup, before any risky changes — this is a step I'm adding to my workflow going forward.

### 5. Documentation
Documenting each step, along with problems, solutions, and screenshots, is a core part of doing cybersecurity work professionally.

---

# 🔐 Security & Ethical Use

This lab is intended strictly for educational and authorized testing purposes only.

---

# 🔗 Tools & Resources

- **VirtualBox:** https://virtualbox.org/wiki/Downloads
- **Kali Linux:** https://kali.org/get-kali

---

# 👤 Author

**[Bilal Ashfaq]**
Cybersecurity Enthusiast / Student

LinkedIn: linkedin.com/in/bilal-siddiqui-61562a333
```

Just make sure your actual screenshot files are placed inside a `screenshots/` folder in the repo with those exact names (or rename yours to match) so the image links resolve correctly on GitHub.
