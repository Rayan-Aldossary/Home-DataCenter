<picture>
  <source media="(prefers-color-scheme: dark)" srcset="banner.svg">
  <source media="(prefers-color-scheme: light)" srcset="banner-light.svg">
  <img src="banner.svg" alt="Home Data Center: a 22U rack with a Cisco ISR 4331, OPNsense on a CloudGenix ION 3000, two Catalyst 3850 switches, a UniFi UNAS Pro and a Dell PowerEdge R720" width="100%">
</picture>

<p align="center">
  <img vspace="3" alt="Cisco IOS XE" src="https://img.shields.io/badge/Cisco-IOS%20XE-049FD9?style=flat-square&logo=cisco&logoColor=white&labelColor=1D1D1D">&nbsp;
  <img vspace="3" alt="OPNsense" src="https://img.shields.io/badge/OPNsense-firewall%20%26%20IDS-D94F00?style=flat-square&logo=opnsense&logoColor=white&labelColor=1D1D1D">&nbsp;
  <img vspace="3" alt="Proxmox VE" src="https://img.shields.io/badge/Proxmox-VE-E57000?style=flat-square&logo=proxmox&logoColor=white&labelColor=1D1D1D">&nbsp;
  <img vspace="3" alt="Windows Server 2022" src="https://img.shields.io/badge/Windows%20Server-2022-0078D4?style=flat-square&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjRkZGRkZGIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCI%2BPHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjE4IiBoZWlnaHQ9IjciIHJ4PSIxLjUiLz48cmVjdCB4PSIzIiB5PSIxNCIgd2lkdGg9IjE4IiBoZWlnaHQ9IjciIHJ4PSIxLjUiLz48Y2lyY2xlIGN4PSI3IiBjeT0iNi41IiByPSIwLjgiIGZpbGw9IiNGRkZGRkYiLz48Y2lyY2xlIGN4PSI3IiBjeT0iMTcuNSIgcj0iMC44IiBmaWxsPSIjRkZGRkZGIi8%2BPC9zdmc%2B&labelColor=1D1D1D">&nbsp;
  <br>
  <img vspace="3" alt="Docker" src="https://img.shields.io/badge/Docker-LibreNMS-2496ED?style=flat-square&logo=docker&logoColor=white&labelColor=1D1D1D">&nbsp;
  <img vspace="3" alt="UniFi" src="https://img.shields.io/badge/UniFi-storage%20%26%20Protect-006FFF?style=flat-square&logo=ubiquiti&logoColor=white&labelColor=1D1D1D">&nbsp;
  <img vspace="3" alt="Ansible" src="https://img.shields.io/badge/Ansible-automation-EE0000?style=flat-square&logo=ansible&logoColor=white&labelColor=1D1D1D">&nbsp;
  <img vspace="3" alt="CCNA certified" src="https://img.shields.io/badge/CCNA-certified-1BA0D7?style=flat-square&logo=cisco&logoColor=white&labelColor=1D1D1D">&nbsp;
</p>

<p align="center">
  <a href="#overview"><b>Overview</b></a> ·
  <a href="#topology"><b>Topology</b></a> ·
  <a href="#walkthrough"><b>Walkthrough</b></a> ·
  <a href="#design-decisions"><b>Design</b></a> ·
  <a href="#hardware"><b>Hardware</b></a> ·
  <a href="#network"><b>Network</b></a> ·
  <a href="#servers"><b>Servers</b></a> ·
  <a href="#security-design"><b>Security</b></a>
</p>

## Overview

A home data center I designed, built and secured in a 22U rack. It runs the same building blocks a business network depends on: Cisco routing and switching, a dedicated firewall, a virtualized Windows Server domain, central storage and security monitoring.

| Networking | Servers & storage | Security |
|-|-|-|
| Cisco ISR 4331 edge router<br>Two Catalyst 3850 switches<br>VLAN segmentation, 20G core uplink | Dell R720 running Proxmox VE<br>Six VMs and an Active Directory domain<br>UniFi UNAS Pro for storage | OPNsense firewall with intrusion detection<br>Wazuh and Splunk Free for logs<br>Isolated guest network |

> [!TIP]
> **New here?** Start with the **Topology** diagram and the **Walkthrough** video for the big picture. **Design decisions** explains why it's built this way. The sections after it hold the details: hardware, addressing, servers and security.

## Lab in numbers

The lab at a glance.

<img src="lab-stats.svg" alt="22U rack, 6 virtual machines, 4 VLANs, 20G LACP uplink, 384 GB hypervisor RAM, 7 NAS drive bays" width="100%">

## Topology

How everything connects, from the internet link down to each VLAN.

<p align="center">
  <img src="topology.svg" alt="Isometric topology: STC modem, Cisco ISR 4331 with NAT, OPNsense on a CloudGenix ION 3000, Catalyst 3850 core and access switches on a 2 x 10G LACP trunk, a VLAN 40 servers area with the Proxmox host and six VMs, UniFi UNAS Pro, UniFi Protect cameras, one UniFi access point with Internal and Guest SSIDs, and client zones for VLANs 10, 20 and 30" width="100%">
</p>

**Reading the diagram:** traffic from the internet comes in through the STC modem and the ISR 4331, passes through OPNsense to be filtered and inspected, then reaches the core switch, which routes it to the right VLAN. The access switch connects every device, and each colored zone is one VLAN.

## Walkthrough

A guided tour of the topology, from the edge router down to every VLAN and virtual machine.

https://github.com/user-attachments/assets/00f0f240-d347-4e98-bb69-2ba5701e0d6b

## Design decisions

Why the network is built the way it is.

- **NAT stays at the edge.** The ISR 4331 owns the internet link and NAT, so OPNsense can filter and inspect traffic without adding a second layer of NAT.
- **Routing happens at the core.** The core 3850 routes between VLANs and relays DHCP requests to Active Directory. The firewall is left to guard traffic going in and out of the network.
- **One 20G uplink.** Two 10G links in an LACP port-channel join the core and access switches, so the link has more bandwidth and keeps working if one cable fails.
- **Split hypervisor networking.** Proxmox itself is managed on VLAN 10, while its VMs use a separate trunk carrying VLANs 20 and 40. Managing the host and serving the VMs never share a link.
- **One AP, two networks.** A single access point broadcasts the Internal and Guest SSIDs, each mapped to its own VLAN (20 and 30).
- **Automation.** Ansible manages device configuration, so changes are repeatable and tracked.

## Hardware

What's in the rack and what each device does.

| Layer | Device | What it does |
|-|-|-|
| Edge | Cisco ISR 4331 | Connects to the internet and runs NAT |
| Firewall | CloudGenix ION 3000 running OPNsense | Filters traffic and runs intrusion detection between the edge router and the core |
| Core | Cisco Catalyst 3850-48 | Layer 3 switch: routes between VLANs and relays DHCP |
| Access | Cisco Catalyst 3850-48 | Layer 2 switch: connects every device, with a 2 × 10G uplink to the core |
| Compute | Dell PowerEdge R720 | Proxmox VE host with dual CPUs and 384 GB of RAM |
| Storage | UniFi UNAS Pro | 7-bay storage for backups, files and camera footage |
| Wireless | UniFi access point | Internal and Guest Wi-Fi from one trunked port |
| Surveillance | UniFi Protect cameras | Video, recorded to the UNAS Pro |
| Power | UniFi UPS and rack PDU | Battery backup and power distribution |

<details>
<summary><b>Rack elevation (22U)</b>, top to bottom</summary>
<br>

| U | Device |
|-|-|
| 19–22 | Reserved |
| 18 | Vented panel |
| 17 | Cisco ISR 4331 |
| 16 | CloudGenix ION 3000 (OPNsense) |
| 15 | Blank panel |
| 14 | Catalyst 3850, core |
| 13 | Blank panel |
| 12 | Catalyst 3850, access |
| 11 | 24-port patch panel |
| 9–10 | UniFi UNAS Pro |
| 7–8 | Dell PowerEdge R720 |
| 6 | PDU |
| 5 | Brush panel |
| 1–4 | Reserved |

</details>

## Network

Each VLAN, what it's for, and how devices on it get their addresses.

| VLAN | Name | Used for | Subnet | Addressing |
|-|-|-|-|-|
| 10 | Management | Network devices, the Proxmox host and the admin workstation | 192.168.10.0/24 | Static |
| 20 | Internal | Trusted users, Internal Wi-Fi and the Windows 11 client | 192.168.20.0/24 | DHCP from SWAGGER-DC-01, relayed by the core |
| 30 | Guest | Visitor Wi-Fi, internet only | 192.168.30.0/24 | DHCP from the core switch |
| 40 | Servers | Virtual machines and the UNAS Pro | 192.168.40.0/24 | Static |
| 999 | Native | Unused on purpose; carries no hosts | None | None |

**Point-to-point links** connect the routing devices in a chain:

| Link | Subnet |
|-|-|
| ISR 4331 to OPNsense | 192.168.60.0/30 |
| OPNsense to core switch | 192.168.50.0/30 |

**Good to know**

- **Gateways:** each VLAN's gateway is the last usable address in its subnet, `.254` (for example `192.168.10.254`), and lives on the core switch.
- **Proxmox:** the host uses two links: an access port on VLAN 10 for managing the host, and a trunk carrying VLANs 20 and 40 for its VMs.
- **Access point:** its switch port is a trunk carrying VLANs 20 and 30, one per SSID.

## Servers

Six virtual machines run on Proxmox: four Windows Server 2022 servers, a Windows 11 client and a Linux Docker host. The Windows machines form the `swagger.lab` Active Directory domain.

| Host | Role | Runs | Address |
|-|-|-|-|
| SWAGGER-DC-01 | Primary domain controller | AD DS, DNS, DHCP, NTP | 192.168.40.1 |
| SWAGGER-DC-02 | Second domain controller | AD DS, DNS | 192.168.40.2 |
| SWAGGER-FS-01 | File server | File shares, WSUS | 192.168.40.3 |
| SWAGGER-CA-01 | Certificate authority | AD CS, NPS (RADIUS) | 192.168.40.4 |
| SWAGGER-NMS-01 | Docker host (Linux) | Containers, listed below | 192.168.40.5 |
| SWAGGER-WKS-01 | Domain client (Windows 11) | Testing logons and group policy | DHCP, VLAN 20 |

### Containers on SWAGGER-NMS-01

The monitoring and security tools run as containers. Each one gets its own IP address on VLAN 40, so it appears on the network as a separate host.

| Container | What it does |
|-|-|
| Portainer | Web interface for managing the containers |
| LibreNMS | Watches every network device over SNMP: health, interface traffic and uptime |
| Wazuh | SIEM: collects logs and agent data, detects threats and checks file integrity |
| Splunk Free | Searches and visualizes the same logs |

## Security design

How the lab is protected, layer by layer.

| Layer | Control | How it works |
|-|-|-|
| Perimeter | Firewall and IDS | OPNsense filters traffic between the edge router and the core, and Suricata inspects it for threats |
| Perimeter | No inbound exposure | No port forwards, no VPN and no public services |
| Network | Segmentation | Management, users, guests and servers each get their own VLAN; the native VLAN carries no hosts |
| Network | Guest isolation | The Guest VLAN reaches the internet only, with its own DHCP on the core switch |
| Identity | Active Directory | Two domain controllers, plus a certificate authority and NPS for RADIUS |
| Endpoints | Patching | WSUS manages Windows updates across the domain |
| Monitoring | Logs and alerts | Wazuh and Splunk Free collect and search logs; LibreNMS watches every device |
| Data | Backups | Servers and files back up to the UNAS Pro, separate from the R720's own drives |
| Physical | Surveillance | UniFi Protect cameras, with footage kept on the UNAS Pro |
| Publishing | Sanitized configs | Configs are cleaned before they're committed; no passwords or secrets live in this repo |

<br>

<p align="center"><sub>Built and documented by <a href="https://github.com/Rayan-Aldossary">Rayan Aldossary</a></sub></p>
