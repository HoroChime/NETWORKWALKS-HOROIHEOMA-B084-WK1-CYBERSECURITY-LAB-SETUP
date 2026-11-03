# NETWORKWALKS-HOROIHEOMA-B084-WK1-CYBERSECURITY-LAB-SETUP
This is my Cybersecurity lab setup for my 1st internship project

Project Overview

A hands-on cybersecurity lab built with Oracle VirtualBox and Kali Linux on a Windows host. The lab uses a dedicated NAT Network to provide Kali Linux with internet access and a defined private IP address.

. Configuration

. Virtualisation: Oracle VirtualBox

. Operating System: Kali Linux

. Network: CyberLab-NAT

. Subnet: 10.0.0.0/24

. Kali IP: 10.0.0.2/24

. Gateway: 10.0.0.1

. DNS: 8.8.8.8

. Network configuration: nmcli

. Shared folder: Windows Downloads folder shared with Kali

. Integration: Bidirectional clipboard and drag-and-drop

. Completed tasks
. Upgraded the virtual box from version 7.2.14 to the latest version 7.2.22
. Configured the private NAT Network on virtualbox enabled in Virtual Machine settings
. Setup the defined network in subnet (
. Configured the defined ipv4 address on kali linux with full internet access (10.0.0.2/24)
. Configured DNS and the default gateway.
. Tested gateway, external IP, and domain-name connectivity using ping.
. Shared folder was enabled with /downloads folder shared from host machine
. Took snapshot of the VM for recovery


Skills Practised

. Linux administration, IPv4 networking, DNS, NAT networking, NetworkManager, virtualisation, and troubleshooting.

Purpose

This lab provides a foundation for authorised cybersecurity practice, including network analysis, security monitoring in a controlled environments.

Note: Testing will be restricted to systems and services I own or have explicit permission to assess.


# 🔐 Cybersecurity Home Lab Setup
### Kali Linux | Oracle VirtualBox | Network Configuration

![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue)
![OS](https://img.shields.io/badge/OS-Kali%20Linux-purple)
![Network](https://img.shields.io/badge/Network-NAT%20Network-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📌 Project Overview

This project documents the setup and configuration of a cybersecurity testing lab using Oracle VirtualBox and Kali Linux on a Windows host machine.

The objective was to establish a functional virtual environment with a dedicated NAT Network, static IP addressing, internet connectivity, DNS configuration, and shared-folder integration.

The lab provides a foundation for future cybersecurity learning, network analysis, and authorised security testing.

---

## 🎯 Project Objectives

The main objectives were to:

- Install and configure Oracle VirtualBox.
- Set up Kali Linux as a virtual machine.
- Create a dedicated VirtualBox NAT Network.
- Configure the network using the `10.0.0.0/24` subnet.
- Assign Kali Linux a static IP address.
- Configure the default gateway and DNS server.
- Verify internet connectivity.
- Enable bidirectional clipboard and drag-and-drop.
- Configure a shared folder between Windows and Kali Linux.
- Manage network settings using `nmcli` commands.

---

## 🏗️ Lab Architecture

| Component | Configuration |
|---|---|
| Host Operating System | Windows |
| Hypervisor | Oracle VirtualBox 7.2.22 |
| Virtual Machine | Kali Linux |
| Network Type | NAT Network |
| NAT Network Name | CyberLab-NAT |
| Network Subnet | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |
| DHCP | Disabled |
| IPv6 | Disabled |
| Shared Folder | CKaliShare |
| Shared Folder Mount | /media/sf_CKaliShare |
| Clipboard | Bidirectional |
| Drag and Drop | Bidirectional |

---

## ⚙️ Lab Setup and Configuration

### Step 1: Install and Upgrade VirtualBox

Installed Oracle VirtualBox and upgraded it to version 7.2.22.

VirtualBox was used as the hypervisor for hosting the Kali Linux virtual machine.

### Step 2: Create a Dedicated NAT Network

Created a NAT Network named `CyberLab-NAT`.

The network was configured with the following parameters:

```bash
VBoxManage natnetwork add \
--netname "CyberLab-NAT" \
--network "10.0.0.0/24" \
--enable \
--dhcp off
```

Network configuration:

- Network: `10.0.0.0/24`
- Gateway: `10.0.0.1`
- DHCP: Disabled
- IPv6: Disabled

### Step 3: Connect Kali Linux to the NAT Network

Configured the first network adapter of the Kali Linux virtual machine to use the newly created NAT Network.

```bash
VBoxManage modifyvm "Kali Linuxx" \
--nic1 natnetwork \
--nat-network1 "CyberLab-NAT" \
--cable-connected1 on
```

### Step 4: Configure a Static IP Address

Used NetworkManager's command-line interface (`nmcli`) to configure Kali Linux with a static IPv4 address.

```bash
sudo nmcli connection modify "Wired connection 1" \
ipv4.method manual \
ipv4.addresses 10.0.0.2/24 \
ipv4.gateway 10.0.0.1 \
ipv4.dns "8.8.8.8"
```

Activated the network connection:

```bash
sudo nmcli connection up "Wired connection 1"
```

### Step 5: Verify Network Configuration

Checked the network interface:

```bash
ip -br address
```

Checked the routing table:

```bash
ip route
```

Verified the DNS configuration:

```bash
nmcli device show eth0 | grep IP4.DNS
```

The configured DNS server was Google Public DNS (`8.8.8.8`).

### Step 6: Test Network and Internet Connectivity

Performed connectivity tests to confirm that Kali Linux could communicate with its gateway and access external networks.

Tested the virtual gateway:

```bash
ping -c 4 10.0.0.1
```

Tested external IP connectivity:

```bash
ping -c 4 8.8.8.8
```

Tested domain name resolution:

```bash
ping -c 4 google.com
```

**Result:** All ping tests were successful.

### Step 7: Configure Shared Folder

Created a shared folder named `CKaliShare` inside the Windows Downloads directory.

Configured the VirtualBox shared-folder settings:

- Folder Name: `CKaliShare`
- Auto-mount: Enabled
- Read-only: Disabled

Verified the shared folder in Kali Linux:

```bash
ls -la /media/sf_CKaliShare
```

Confirmed that the current Kali Linux user belonged to the `vboxsf` group:

```bash
groups
```

### Step 8: Enable VirtualBox Integration Features

Configured the following VirtualBox settings:

- Shared Clipboard: Bidirectional
- Drag and Drop: Bidirectional

These settings support file transfer and clipboard sharing between the Windows host and Kali Linux guest.

---

## 🔎 Lab Verification Summary

| Test | Command / Check | Result |
|---|---|---|
| IP Address | `ip -br address` | Successful |
| Default Gateway | `ip route` | Successful |
| Gateway Connectivity | `ping -c 4 10.0.0.1` | Successful |
| External Connectivity | `ping -c 4 8.8.8.8` | Successful |
| DNS Resolution | `ping -c 4 google.com` | Successful |
| DNS Configuration | `nmcli device show eth0` | Successful |
| Shared Folder | `ls -la /media/sf_CKaliShare` | Verified |
| User Group | `groups` | `vboxsf` present |

---

## 📸 Project Screenshots

Screenshots documenting the configuration and verification process are included below.

### 1. VirtualBox NAT Network Configuration

![VirtualBox NAT Network](screenshots/01-virtualbox-nat-network.png)

### 2. Kali Linux IP Address Configuration

![Kali IP Configuration](screenshots/02-kali-ip-configuration.png)

### 3. Internet Connectivity Test

![Internet Connectivity](screenshots/03-internet-connectivity.png)

### 4. DNS Configuration Using nmcli

![DNS Configuration](screenshots/04-dns-configuration.png)

### 5. Shared Folder Configuration

![Shared Folder](screenshots/05-shared-folder.png)

### 6. VirtualBox Clipboard and Drag-and-Drop Settings

![VirtualBox Integration Settings](screenshots/06-virtualbox-integration.png)

---

## 💡 Key Skills and Knowledge Gained

Through this hands-on exercise, I strengthened my understanding of:

1. Virtualisation and virtual machine management.
2. VirtualBox NAT Network configuration.
3. IPv4 addressing and subnetting.
4. Static IP and default gateway configuration.
5. DNS configuration and domain name resolution.
6. Linux network administration using `nmcli`.
7. Network connectivity testing and troubleshooting.
8. Windows and Linux shared-folder integration.

### Understanding nmcli

One of the important tools used during this exercise was `nmcli` (NetworkManager Command-Line Interface).

It allows network connections and configurations to be managed directly from the Linux terminal.

---

## 🔐 Security and Ethical Use

This lab is intended for educational purposes and authorised cybersecurity testing.

Any future security assessments will be conducted only against systems I own or have explicit permission to test.

---

## 🔗 Tools and Resources

- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux](https://www.kali.org/get-kali/)
- [NetworkManager Documentation](https://networkmanager.dev/docs/)

---

## 🚀 Next Steps

The next phase of this project will focus on expanding the virtual lab environment and documenting additional cybersecurity exercises, including network analysis, security monitoring, and vulnerability assessment.

---

## 👤 Author

**Horoiheoma Lazarus Chimezie**

Cybersecurity Enthusiast | Security Operations | Network Security

---

*Hands-on learning. Practical experience. Continuous improvement.*


