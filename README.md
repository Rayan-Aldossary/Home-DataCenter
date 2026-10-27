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

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/overview-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/overview-light.svg">
  <img src="assets/overview-light.svg" alt="Overview: Networking with a Cisco ISR 4331, two Catalyst 3850 switches, 4 VLANs and a 20G core uplink. Servers and storage with a Dell R720 running Proxmox, six VMs in an Active Directory domain and a UniFi UNAS Pro. Security with an OPNsense firewall and Suricata IDS, Wazuh and Splunk Free, and isolated guest Wi-Fi." width="100%">
</picture>

> [!TIP]
> **New here?** Start with the **Topology** diagram and the **Walkthrough** video for the big picture. **Design decisions** explains why it's built this way. The sections after it hold the details: hardware, network, servers and security.

## Lab in numbers

The lab at a glance.

<img src="lab-stats.svg" alt="22U rack, 6 virtual machines, 4 VLANs, 20G LACP uplink, 384 GB hypervisor RAM, 7 NAS drive bays" width="100%">

## Topology

How everything connects, from the internet link down to each VLAN.

<p align="center">
  <img src="topology.svg" alt="Isometric topology: STC modem, Cisco ISR 4331 with NAT, OPNsense on a CloudGenix ION 3000, Catalyst 3850 core and access switches on a 2 x 10G LACP trunk, a VLAN 40 servers area with the Proxmox host and six VMs, UniFi UNAS Pro, UniFi Protect cameras, one UniFi access point with Internal and Guest SSIDs, and client zones for VLANs 10, 20 and 30" width="100%">
</p>

> [!NOTE]
> **Reading the diagram:** traffic from the internet comes in through the STC modem and the ISR 4331, passes through OPNsense to be filtered and inspected, then reaches the core switch, which routes it to the right VLAN. The access switch connects every device, and each colored zone is one VLAN.

## Walkthrough

A guided tour of the topology, from the edge router down to every VLAN and virtual machine.

https://github.com/user-attachments/assets/00f0f240-d347-4e98-bb69-2ba5701e0d6b

## Design decisions

Why the network is built the way it is.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/design-decisions-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/design-decisions-light.svg">
  <img src="assets/design-decisions-light.svg" alt="Design decisions: NAT stays at the edge. The ISR 4331 owns the internet link and runs NAT, so OPNsense can filter and inspect traffic without adding a second layer of NAT. Routing happens at the core. The core 3850 routes between VLANs and relays DHCP to Active Directory, leaving the firewall to guard traffic in and out of the network. One 20G uplink. Two 10G links in an LACP port-channel join the core and access switches. That doubles the bandwidth, and the uplink stays up if one cable fails. Split hypervisor networking. Proxmox is managed on VLAN 10, while its VMs use a separate trunk for VLANs 20 and 40, so host management never shares a link with VM traffic. One AP, two networks. One access point broadcasts the Internal and Guest SSIDs. Each SSID maps to its own VLAN, and both ride a single trunked switch port. Automation. Ansible manages device configuration, so every change is repeatable, reviewable and tracked." width="100%">
</picture>

## Hardware

What's in the rack and what each device does. The chip in each corner is the device's position in the rack.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/hardware-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/hardware-light.svg">
  <img src="assets/hardware-light.svg" alt="Hardware: Edge: Cisco ISR 4331. Internet link and NAT. Hands traffic to the firewall over a /30 transit link. Firewall: CloudGenix ION 3000. Runs OPNsense: stateful filtering and Suricata intrusion detection between the edge and the core. Core: Catalyst 3850-48. Layer 3 switch. Routes between VLANs and relays DHCP to Active Directory. Access: Catalyst 3850-48. Layer 2 switch. Connects every device, with a 2 × 10G LACP uplink to the core. Compute: Dell PowerEdge R720. Proxmox VE host with dual CPUs and 384 GB of RAM, running six VMs. Storage: UniFi UNAS Pro. Seven-bay storage for backups, shared files and all camera footage. Wireless: UniFi access point. Internal and Guest Wi-Fi from one trunked switch port. Surveillance: UniFi Protect cameras. Cameras powered over the switch port, recording footage to the UNAS Pro. Power: UniFi UPS and rack PDU. Battery backup and power distribution for the whole rack." width="100%">
</picture>

### Rack elevation

The 22U rack, front view, from top to bottom. The colored edge on each device matches its layer above.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/rack-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/rack-light.svg">
  <img src="assets/rack-light.svg" alt="Rack elevation, 22U, top to bottom: U19 to 22 reserved, U18 vented panel, U17 Cisco ISR 4331, U16 CloudGenix ION 3000 running OPNsense, U15 blank panel, U14 core Catalyst 3850, U13 blank panel, U12 access Catalyst 3850, U11 24-port patch panel, U9 to 10 UniFi UNAS Pro, U7 to 8 Dell PowerEdge R720, U6 PDU, U5 brush panel, U1 to 4 reserved." width="100%">
</picture>

## Network

Four VLANs split the network by role. Each card shows the subnet, the gateway and how devices on it get their addresses.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/vlans-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/vlans-light.svg">
  <img src="assets/vlans-light.svg" alt="VLANs. 10 Management: 192.168.10.0/24, gateway .254, static, for switches, the Proxmox host and the admin workstation. 20 Internal: 192.168.20.0/24, gateway .254, DHCP from SWAGGER-DC-01 relayed by the core, for trusted users, Internal Wi-Fi and WKS-01. 30 Guest: 192.168.30.0/24, gateway .254, DHCP pool on the core switch, visitor Wi-Fi with internet only. 40 Servers: 192.168.40.0/24, gateway .254, static, for virtual machines and the UNAS Pro. Native VLAN 999 carries no hosts." width="100%">
</picture>

### Backbone links

The chain from the internet to the access switch. Each routed hop is its own /30 point-to-point subnet, and the two switches are joined by a 2 × 10G port-channel.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/backbone-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/backbone-light.svg">
  <img src="assets/backbone-light.svg" alt="Backbone links: STC modem to ISR 4331 Gi0/0/1 over DHCP; ISR Gi0/0/0 192.168.60.1 to OPNsense WAN 192.168.60.2 on 192.168.60.0/30; OPNsense LAN 192.168.50.1 to core switch Gi1/0/1 192.168.50.2 on 192.168.50.0/30; core Te1/0/1-2 to access Te1/0/1-2 as port-channel 1, 2 x 10G LACP trunk." width="100%">
</picture>

### Access switch ports

Every device plugs into the access switch. Access ports carry one VLAN; trunk ports carry several.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/switch-ports-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/switch-ports-light.svg">
  <img src="assets/switch-ports-light.svg" alt="Access switch ports: Gi1/0/1 access VLAN 10 admin workstation; Gi1/0/2 trunk 20 and 30 UniFi access point; Gi1/0/3 access VLAN 20 internal workstation; Gi1/0/4-5 PoE UniFi Protect cameras; Gi1/0/10 access VLAN 10 R720 NIC1 Proxmox management; Gi1/0/11 trunk 20 and 40 R720 NIC2 VM traffic; Gi1/0/12 access VLAN 40 UniFi UNAS Pro; all other ports shut down; Te1/0/1-2 LACP trunk to the core switch." width="100%">
</picture>

> [!NOTE]
> **Good to know:** every gateway is the last usable address in its subnet (`.254`) and lives on the core switch. Trunks carry only the VLANs they need: VLANs 20 and 40 to Proxmox, VLANs 20 and 30 to the access point.

## Servers

Six virtual machines run on Proxmox: four Windows Server 2022 servers, a Windows 11 client and a Linux Docker host. The Windows machines form the `swagger.lab` Active Directory domain.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/servers-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/servers-light.svg">
  <img src="assets/servers-light.svg" alt="Proxmox host pve.swagger.lab on a Dell PowerEdge R720: vmbr0 management 192.168.10.3, vmbr1 VM trunk for VLANs 20 and 40, 384 GB of memory. Virtual machines: SWAGGER-DC-01, Primary domain controller, AD DS, DNS, DHCP, NTP, Windows Server 2022, 192.168.40.1; SWAGGER-DC-02, Second domain controller, AD DS, DNS, Windows Server 2022, 192.168.40.2; SWAGGER-FS-01, File server and patching, File shares, WSUS, Windows Server 2022, 192.168.40.3; SWAGGER-CA-01, PKI and network policy, AD CS, NPS (RADIUS), Windows Server 2022, 192.168.40.4; SWAGGER-NMS-01, Docker host, monitoring and SIEM, Docker, Portainer, LibreNMS, Wazuh, Splunk, Linux, 192.168.40.5; SWAGGER-WKS-01, Domain-joined test client, Logons, Group Policy, Windows 11, DHCP." width="100%">
</picture>

> [!NOTE]
> **SWAGGER-WKS-01 is a VM, not a physical PC.** It runs on the same Proxmox host as the servers, but its network card sits on the VLAN 20 side of the trunk, so it behaves like any other Internal client and gets its address by DHCP from SWAGGER-DC-01.

### Containers on SWAGGER-NMS-01

The monitoring and security tools run as Docker containers on SWAGGER-NMS-01.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/containers-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/containers-light.svg">
  <img src="assets/containers-light.svg" alt="Docker host SWAGGER-NMS-01 at 192.168.40.5 on a macvlan network, each tool with its own VLAN 40 address. Containers: Wazuh: SIEM: collects logs and agent data, detects threats and checks file integrity.; Splunk Free: Searches, dashboards and reports over the same logs.; LibreNMS: Watches every switch, router and the firewall over SNMP: health, traffic and uptime.; Portainer: Web interface for managing every container on the host." width="100%">
</picture>

## Security design

How the lab is protected, layer by layer. The zones run from least trusted on the left to most trusted on the right.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/trust-zones-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/trust-zones-light.svg">
  <img src="assets/trust-zones-light.svg" alt="Trust zones, least to most trusted. Zone 1 Untrusted: the internet via STC. Zone 2 Perimeter: the ISR 4331 doing NAT, then the OPNsense firewall with Suricata IDS on a CloudGenix ION 3000. Zone 3 Trusted LAN: core and access switches with VLAN 10 Management, VLAN 20 Internal and VLAN 40 Servers routed at the core, and VLAN 30 Guest limited to the internet. Zone 4 Management: SSH access limited by the Admin-SSH access list to the admin workstation at 192.168.10.1." width="100%">
</picture>

Zone 4 isn't a separate cable path. It's a privilege boundary enforced by an access list on every network device.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/security-controls-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/security-controls-light.svg">
  <img src="assets/security-controls-light.svg" alt="Security controls in place: Perimeter, Firewall and IDS: OPNsense filters traffic between the edge and the core; Suricata inspects it.; Perimeter, No inbound exposure: No port forwards, no VPN and no public services.; Network, Segmentation: Each role gets its own VLAN; the native VLAN carries no hosts.; Network, Guest isolation: Guest Wi-Fi reaches the internet only, with DHCP from the core switch.; Access, Admin-only SSH: Network devices accept SSH only from the admin workstation.; Identity, Active Directory: Two domain controllers, a certificate authority and NPS for RADIUS.; Endpoints, Patching: WSUS manages Windows updates across the domain.; Monitoring, Logs and alerts: Wazuh and Splunk Free collect and search logs; LibreNMS watches every device.; Data, Backups: Servers and files back up to the UNAS Pro, off the R720&#x27;s own drives.; Physical, Surveillance: UniFi Protect cameras record to the UNAS Pro.; Publishing, Sanitized configs: Configs are cleaned before they&#x27;re committed; no passwords or secrets here." width="100%">
</picture>

<br>

<p align="center"><sub>Built and documented by <a href="https://github.com/Rayan-Aldossary">Rayan Aldossary</a></sub></p>
