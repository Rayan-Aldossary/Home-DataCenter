<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/banner-light.svg">
  <img src="assets/banner.svg" alt="Home Data Center: a 22U rack with a Cisco ISR 4331, OPNsense on a CloudGenix ION 3000, two Catalyst 3850 switches, a UniFi UNAS Pro and a Dell PowerEdge R720" width="100%">
</picture>

<br>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/label-built-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/label-built-light.svg">
  <img src="assets/label-built-light.svg" alt="Built with" width="720">
</picture>
</p>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/stack-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/stack-light.svg">
  <img src="assets/stack-light.svg" alt="Built with Cisco IOS XE, OPNsense firewall and IDS, Proxmox VE, Windows Server 2022, Docker, UniFi storage and Wi-Fi, Ansible automation, Wazuh SIEM, Splunk log analytics and LibreNMS network monitoring." width="702">
</picture>
</p>

<br>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/label-jump-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/label-jump-light.svg">
  <img src="assets/label-jump-light.svg" alt="Jump to a section" width="720">
</picture>
</p>

<p align="center">
<a href="#overview"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-overview-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-overview-light.svg"><img src="assets/nav-overview-light.svg" alt="Overview" height="40" vspace="5"></picture></a>&nbsp;
<a href="#topology"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-topology-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-topology-light.svg"><img src="assets/nav-topology-light.svg" alt="Topology" height="40" vspace="5"></picture></a>&nbsp;
<a href="#walkthrough"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-walkthrough-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-walkthrough-light.svg"><img src="assets/nav-walkthrough-light.svg" alt="Walkthrough" height="40" vspace="5"></picture></a>&nbsp;
<a href="#design-decisions"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-design-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-design-light.svg"><img src="assets/nav-design-light.svg" alt="Design" height="40" vspace="5"></picture></a>&nbsp;
<a href="#hardware"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-hardware-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-hardware-light.svg"><img src="assets/nav-hardware-light.svg" alt="Hardware" height="40" vspace="5"></picture></a>&nbsp;
<br>
<a href="#rack-elevation"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-rack-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-rack-light.svg"><img src="assets/nav-rack-light.svg" alt="Rack" height="40" vspace="5"></picture></a>&nbsp;
<a href="#network"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-network-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-network-light.svg"><img src="assets/nav-network-light.svg" alt="Network" height="40" vspace="5"></picture></a>&nbsp;
<a href="#servers"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-servers-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-servers-light.svg"><img src="assets/nav-servers-light.svg" alt="Servers" height="40" vspace="5"></picture></a>&nbsp;
<a href="#domain-and-email"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-domain-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-domain-light.svg"><img src="assets/nav-domain-light.svg" alt="Domain" height="40" vspace="5"></picture></a>&nbsp;
<a href="#security-design"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav-security-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/nav-security-light.svg"><img src="assets/nav-security-light.svg" alt="Security" height="40" vspace="5"></picture></a>&nbsp;
</p>

<br>

## <a name="overview"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-overview-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-overview-light.svg"><img src="assets/h-overview-light.svg" height="32" align="top" alt=""></picture>Overview

A home data center I designed, built and secured myself, to run and protect my own services at home. Everything lives in a single rack, and each part is explained in the sections below.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/overview-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/overview-light.svg">
  <img src="assets/overview-light.svg" alt="Overview: Networking with a Cisco ISR 4331, two Catalyst 3850 switches, 5 VLANs and a 20G core uplink. Servers and storage with a Dell R720 running Proxmox, six VMs in an Active Directory domain and a UniFi UNAS Pro. Security with an OPNsense firewall and Suricata IDS, Wazuh and Splunk Free, and isolated guest Wi-Fi." width="100%">
</picture>

> [!TIP]
> **New here?** Start with the **Topology** diagram and the **Walkthrough** video for the big picture. **Design decisions** explains why it's built this way. The sections after it hold the details: hardware, network, servers, domain and security.

<br>

## <a name="lab-in-numbers"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-lab-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-lab-light.svg"><img src="assets/h-lab-light.svg" height="32" align="top" alt=""></picture>Lab in numbers

The lab at a glance.

<img src="assets/lab-stats.svg" alt="22U rack, 6 virtual machines, 5 VLANs, 20G LACP uplink, 384 GB hypervisor RAM, 7 NAS drive bays" width="100%">

<br>

<br>

## <a name="topology"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-topology-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-topology-light.svg"><img src="assets/h-topology-light.svg" height="32" align="top" alt=""></picture>Topology

How everything connects, from the internet link down to each VLAN.

<p align="center">
  <img src="assets/topology.svg" alt="Isometric topology: STC modem, Cisco ISR 4331 with NAT, OPNsense on a CloudGenix ION 3000, Catalyst 3850 core and access switches on a 2 x 10G LACP trunk, a VLAN 40 servers area with the Proxmox host and six VMs, UniFi UNAS Pro, a VLAN 50 camera area with four PoE cameras and an NVR, two UniFi access points with Internal and Guest SSIDs and 802.11r roaming, and client zones for VLANs 10, 20 and 30" width="100%">
</p>

> [!NOTE]
> **Reading the diagram:** traffic from the internet comes in through the STC modem and the ISR 4331, passes through OPNsense to be filtered and inspected, then reaches the core switch, which routes it to the right VLAN. The access switch connects every device, and each colored zone is one VLAN.

<br>

## <a name="walkthrough"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-walkthrough-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-walkthrough-light.svg"><img src="assets/h-walkthrough-light.svg" height="32" align="top" alt=""></picture>Walkthrough

A guided tour of the topology, from the edge router down to every VLAN and virtual machine.

https://github.com/user-attachments/assets/00f0f240-d347-4e98-bb69-2ba5701e0d6b

<br>

## <a name="design-decisions"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-design-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-design-light.svg"><img src="assets/h-design-light.svg" height="32" align="top" alt=""></picture>Design decisions

Why the network is built the way it is.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/design-decisions-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/design-decisions-light.svg">
  <img src="assets/design-decisions-light.svg" alt="Design decisions: NAT stays at the edge. The STC modem and the ISR 4331 handle NAT. OPNsense adds none of its own, so it filters and inspects traffic with the real internal addresses. Routing happens at the core. The core 3850 is the gateway for every VLAN and relays DHCP, leaving the firewall to guard traffic in and out of the network. One 20G uplink. Two 10G links in an LACP port-channel join the core and access switches. That doubles the bandwidth, and the uplink stays up if one cable fails. Split hypervisor networking. Proxmox is managed on VLAN 10, while its VMs use a separate trunk for VLANs 20 and 40, so host management never shares a link with VM traffic. Two APs, two networks. An access point on each floor broadcasts the Internal and Guest SSIDs, each mapped to its own VLAN. 802.11r lets devices roam between floors without dropping. Two DHCP servers, one relay. The core relays every DHCP request. Internal clients get addresses from the domain controller, while guests and cameras get theirs from OPNsense, so neither ever talks to a server. Guests and cameras kept apart. Access lists on the core keep both VLANs away from the trusted networks. Guests only reach the internet, and the admin workstation can still reach in to manage the cameras. Automation. Ansible manages device configuration, so every change is repeatable, reviewable and tracked." width="100%">
</picture>

<br>

## <a name="hardware"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-hardware-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-hardware-light.svg"><img src="assets/h-hardware-light.svg" height="32" align="top" alt=""></picture>Hardware

What's in the rack and what each device does. The chip in each corner is the device's position in the rack.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/hardware-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/hardware-light.svg">
  <img src="assets/hardware-light.svg" alt="Hardware: Edge: Cisco ISR 4331. Internet link and NAT. Hands traffic to the firewall over a /30 transit link. Firewall: CloudGenix ION 3000. Runs OPNsense: stateful filtering, Suricata IDS, and DHCP for the Guest and camera VLANs. Core: Catalyst 3850-48. Layer 3 switch that routes between VLANs and relays DHCP requests. Access: Catalyst 3850-48. Layer 2 switch for every device, with a 2 × 10G uplink to the core. Compute: Dell PowerEdge R720. Proxmox VE host with dual CPUs and 384 GB of RAM, running six VMs. Storage: UniFi UNAS Pro. Seven-bay storage for backups and file shares. Wireless: Two UniFi access points. One per floor, each with Internal and Guest Wi-Fi and fast roaming. Surveillance: PoE cameras and NVR. Four cameras on their own VLAN, recording to the NVR in the rack. Power: UniFi UPS and rack PDU. Battery backup and power distribution for the whole rack." width="100%">
</picture>

<br>

## <a name="rack-elevation"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-rack-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-rack-light.svg"><img src="assets/h-rack-light.svg" height="32" align="top" alt=""></picture>Rack elevation

The 22U rack, front view, from top to bottom. The colored edge on each device matches its layer above.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/rack-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/rack-light.svg">
  <img src="assets/rack-light.svg" alt="Rack elevation, 22U, top to bottom: U19 to 22 reserved, U18 vented panel, U17 Cisco ISR 4331, U16 CloudGenix ION 3000 running OPNsense, U15 NVR for camera recording, U14 core Catalyst 3850, U13 blank panel, U12 access Catalyst 3850, U11 24-port patch panel, U9 to 10 UniFi UNAS Pro, U7 to 8 Dell PowerEdge R720, U6 PDU, U5 brush panel, U1 to 4 reserved." width="100%">
</picture>

<br>

## <a name="network"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-network-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-network-light.svg"><img src="assets/h-network-light.svg" height="32" align="top" alt=""></picture>Network

Five VLANs split the network by role, plus a native VLAN that carries no hosts. Each card shows the subnet, the gateway and how devices on it get their addresses.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/vlans-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/vlans-light.svg">
  <img src="assets/vlans-light.svg" alt="VLANs. 10 Management: 192.168.10.0/24, gateway .254, static, for switches, the access points, the Proxmox host and the admin workstation. 20 Internal: 192.168.20.0/24, gateway .254, DHCP from SWAGGER-DC-01 relayed by the core, for trusted users, Internal Wi-Fi and WKS-01. 30 Guest: 192.168.30.0/24, gateway .254, DHCP from OPNsense relayed by the core, visitor Wi-Fi with internet only. 40 Servers: 192.168.40.0/24, gateway .254, static, for virtual machines and the UNAS Pro. 50 Cameras: 172.16.0.0/27, gateway 172.16.0.30, DHCP from OPNsense relayed by the core, for four PoE cameras and the NVR. Native VLAN 999: no subnet and no hosts, native on every trunk except the access point ports." width="100%">
</picture>

<br>

## <a name="backbone-links"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-backbone-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-backbone-light.svg"><img src="assets/h-backbone-light.svg" height="32" align="top" alt=""></picture>Backbone links

How traffic gets from the internet to the access switch. Each card is a device and each line is a cable. Where a cable meets a card, the tag shows that device's port and IP; the label on the cable is the link's subnet.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/backbone-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/backbone-light.svg">
  <img src="assets/backbone-light.svg" alt="Backbone links, top to bottom. STC modem LAN port to SWAGGER-4331-ISR01 Gi0/0/1 over DHCP, 1 GbE. ISR Gi0/0/0 192.168.50.1 to OPNsense firewall WAN 192.168.50.2 on 192.168.50.0/30, 1 GbE. OPNsense LAN 192.168.50.5 to SWAGGER-CORE-SW01 Gi1/0/1 192.168.50.6 on 192.168.50.4/30, a point-to-point routed link, 1 GbE. Core Te1/0/1-2 to SWAGGER-ACCESS-SW01 Te1/0/1-2 as port-channel 1, a 2 x 10G LACP trunk carrying all VLANs." width="100%">
</picture>

<br>

## <a name="access-switch-ports"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-ports-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-ports-light.svg"><img src="assets/h-ports-light.svg" height="32" align="top" alt=""></picture>Access switch ports

Every device plugs into the access switch, always on the top row (odd ports). Access ports carry one VLAN; trunk ports carry several.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/switch-ports-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/switch-ports-light.svg">
  <img src="assets/switch-ports-light.svg" alt="Access switch ports, all on the top row (odd numbers): Gi1/0/1 access VLAN 10 admin workstation; Gi1/0/3 trunk 20 and 30 UniFi AP-1, ground floor, native VLAN 10; Gi1/0/5 trunk 20 and 30 UniFi AP-2, first floor, native VLAN 10; Gi1/0/7 access VLAN 20 internal workstation; Gi1/0/9, 11, 13 and 15 access VLAN 50 PoE cameras; Gi1/0/17 access VLAN 50 NVR; Gi1/0/19 access VLAN 10 R720 NIC1 Proxmox management; Gi1/0/21 trunk 20 and 40 R720 NIC2 VM traffic; Gi1/0/23 access VLAN 40 UniFi UNAS Pro; even ports and ports 25 to 48 shut down; Te1/0/1-2 LACP trunk to the core switch." width="100%">
</picture>

How it's cabled: every device uses an odd port on the switch's top row, so each cord drops straight down to the patch panel port below it (panel 1 to Gi1/0/1, panel 2 to Gi1/0/3, and so on). Every cord has a flag label with its panel port and device, cord colors follow the VLANs, and trunk cords are striped with the VLANs they carry.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/cabling-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/cabling-light.svg">
  <img src="assets/cabling-light.svg" alt="Cabling, front view of U11 and U12. Every device uses an odd port on the top row of the access switch SWAGGER-ACCESS-SW01, and each cord drops straight down to the patch panel port below it: panel port N connects to switch port 2N minus 1. Every cord carries a flag label with its panel port and device. Panel 1 to Gi1/0/1, admin PC, VLAN 10. Panel 2 to Gi1/0/3, AP-1, trunk for VLANs 20 and 30. Panel 3 to Gi1/0/5, AP-2, trunk for VLANs 20 and 30. Panel 4 to Gi1/0/7, internal PC, VLAN 20. Panels 5 to 8 to Gi1/0/9, 11, 13 and 15, four PoE cameras, VLAN 50. Panel 9 to Gi1/0/17, NVR, VLAN 50. Panel 10 to Gi1/0/19, R720 NIC1, VLAN 10. Panel 11 to Gi1/0/21, R720 NIC2, trunk for VLANs 20 and 40. Panel 12 to Gi1/0/23, UNAS Pro, VLAN 40. Even ports and ports 25 to 48 are shut down. Te1/0/1-2 uplink to the core as Po1. Panel ports 1 to 8 are wall runs, 9 to 12 come from devices in the rack, and 13 to 24 are spare. Cord colors follow the VLANs; trunk cords are striped." width="100%">
</picture>

> [!NOTE]
> **Good to know:** every gateway is the last usable address in its subnet (`.254`, or `172.16.0.30` for the cameras). The core switch is the gateway for every VLAN and relays all DHCP: Internal clients get addresses from SWAGGER-DC-01, while Guest and Cameras get theirs from OPNsense. Management and Servers use static addresses. The camera VLAN uses its own private range, `172.16.0.0/27`, so it stays visibly separate from the `192.168` networks. Trunks carry only the VLANs they need: VLANs 20 and 40 to Proxmox, and VLANs 20 and 30 to each access point. The access points take their own management address untagged, on native VLAN 10.

<br>

## <a name="servers"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-servers-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-servers-light.svg"><img src="assets/h-servers-light.svg" height="32" align="top" alt=""></picture>Servers

Six virtual machines run on Proxmox: four Windows Server 2022 servers, a Windows 11 client and a Linux Docker host. The Windows machines form the `swagger.rayanaldossary.com` Active Directory domain.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/servers-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/servers-light.svg">
  <img src="assets/servers-light.svg" alt="Proxmox host pve.swagger.rayanaldossary.com on a Dell PowerEdge R720: vmbr0 management 192.168.10.3, vmbr1 VM trunk for VLANs 20 and 40, 384 GB of memory. Virtual machines: SWAGGER-DC-01, Primary domain controller, AD DS, DNS, DHCP, NTP, Windows Server 2022, 192.168.40.1; SWAGGER-DC-02, Second domain controller, AD DS, DNS, Windows Server 2022, 192.168.40.2; SWAGGER-FS-01, File server and patching, File shares, WSUS, Windows Server 2022, 192.168.40.3; SWAGGER-CA-01, PKI and network policy, AD CS, NPS (RADIUS), Windows Server 2022, 192.168.40.4; SWAGGER-NMS-01, Docker host, monitoring and SIEM, Docker, Portainer, LibreNMS, Wazuh, Splunk, Linux, 192.168.40.5; SWAGGER-WKS-01, Domain-joined test client, Logons, Group Policy, Windows 11, DHCP." width="100%">
</picture>

> [!NOTE]
> **SWAGGER-WKS-01 is a VM, not a physical PC.** It runs on the same Proxmox host as the servers, but its network card sits on the VLAN 20 side of the trunk, so it behaves like any other Internal client and gets its address by DHCP from SWAGGER-DC-01.

<br>

## <a name="containers-on-swagger-nms-01"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-containers-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-containers-light.svg"><img src="assets/h-containers-light.svg" height="32" align="top" alt=""></picture>Containers on SWAGGER-NMS-01

The monitoring and security tools run as Docker containers on SWAGGER-NMS-01.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/containers-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/containers-light.svg">
  <img src="assets/containers-light.svg" alt="Docker host SWAGGER-NMS-01 at 192.168.40.5 on a macvlan network, each tool with its own VLAN 40 address. Containers: Wazuh: SIEM: collects logs and agent data, detects threats and checks file integrity.; Splunk Free: Searches, dashboards and reports over the same logs.; LibreNMS: Watches every switch, router and the firewall over SNMP: health, traffic and uptime.; Portainer: Web interface for managing every container on the host." width="100%">
</picture>

<br>

## <a name="domain-and-email"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-domain-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-domain-light.svg"><img src="assets/h-domain-light.svg" height="32" align="top" alt=""></picture>Domain and email

The lab runs under my own domain, `rayanaldossary.com`. Its public DNS and email live on Cloudflare and Google Workspace. Active Directory uses a subdomain of it, `swagger.rayanaldossary.com`, which only resolves inside the lab.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/domain-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/domain-light.svg">
  <img src="assets/domain-light.svg" alt="Domain and email. Public domain rayanaldossary.com: registrar Cloudflare, DNS on Cloudflare, email on Google Workspace. Internal domain swagger.rayanaldossary.com, a subdomain of it: DNS served by Active Directory on DC-01 and DC-02, resolves only inside the lab, and every Windows machine is a member. Mail DNS records on Cloudflare: MX at @: smtp.google.com · priority 10, Routes mail to Google Workspace; TXT at @: v=spf1 include:_spf.google.com ~all, SPF: only Google may send as the domain; TXT at google._domainkey: v=DKIM1; k=rsa; p=… (Google key), DKIM: signs every outgoing message; TXT at _dmarc: v=DMARC1; p=none; rua=mailto:rayan@…, DMARC: monitors and reports spoofing; TXT at @: google-site-verification=…, Proves domain ownership to Google." width="100%">
</picture>

> [!NOTE]
> **Why a subdomain?** Microsoft recommends naming an Active Directory domain after a subdomain of a domain you own, instead of an invented suffix like `.local` or `.lab`. That way, internal names can never clash with anyone else's on the internet.

<br>

## <a name="security-design"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-security-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-security-light.svg"><img src="assets/h-security-light.svg" height="32" align="top" alt=""></picture>Security design

How the lab is protected, layer by layer. The zones run from least trusted on the left to most trusted on the right.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/trust-zones-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/trust-zones-light.svg">
  <img src="assets/trust-zones-light.svg" alt="Trust zones, least to most trusted. Zone 1 Untrusted: the internet via STC. Zone 2 Perimeter: the ISR 4331 doing NAT, then the OPNsense firewall with Suricata IDS on a CloudGenix ION 3000. Zone 3 Trusted LAN: core and access switches with VLAN 10 Management, VLAN 20 Internal and VLAN 40 Servers routed at the core, VLAN 50 Cameras isolated from the servers, and VLAN 30 Guest limited to the internet. Zone 4 Management: SSH access limited by the Admin-SSH access list to the admin workstation at 192.168.10.1." width="100%">
</picture>

Zone 4 isn't a separate cable path. It's a privilege boundary enforced by an access list on every network device.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/security-controls-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/security-controls-light.svg">
  <img src="assets/security-controls-light.svg" alt="Security controls in place: Perimeter, Firewall and IDS: OPNsense filters traffic between the edge and the core; Suricata inspects it.; Perimeter, No inbound exposure: No port forwards, no VPN and no public services.; Network, Segmentation: Each role gets its own VLAN; the native VLAN carries no hosts.; Network, Guest isolation: Guest Wi-Fi reaches the internet only; its DHCP comes from OPNsense.; Network, Camera isolation: Cameras can&#x27;t reach the trusted VLANs; the admin workstation can reach in.; Access, Admin-only SSH: Network devices accept SSH only from the admin workstation.; Identity, Active Directory: Two domain controllers, a certificate authority and NPS for RADIUS.; Endpoints, Patching: WSUS manages Windows updates across the domain.; Monitoring, Logs and alerts: Wazuh and Splunk Free collect and search logs; LibreNMS watches every device.; Data, Backups: Servers and files back up to the UNAS Pro, off the R720&#x27;s own drives.; Physical, Surveillance: Four PoE cameras on their own VLAN, recording to the NVR.; Publishing, Sanitized configs: Configs are cleaned before they&#x27;re committed; no passwords or secrets here." width="100%">
</picture>

<br>

## <a name="detection-pipeline"></a><picture><source media="(prefers-color-scheme: dark)" srcset="assets/h-pipeline-dark.svg"><source media="(prefers-color-scheme: light)" srcset="assets/h-pipeline-light.svg"><img src="assets/h-pipeline-light.svg" height="32" align="top" alt=""></picture>Detection pipeline

The lab's devices send their logs to Wazuh, which runs in Docker on SWAGGER-NMS-01. The animation follows one attack from start to finish: a brute-force login attempt on SWAGGER-DC-01 raises a level 10 alert, Wazuh blocks the source, and the alert is forwarded to Splunk.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/pipeline-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/pipeline-light.svg">
  <img src="assets/pipeline-light.svg" alt="Detection pipeline. Five log sources feed Wazuh: the Cisco network (ISR 4331 and Catalyst 3850s), OPNsense with Suricata (firewall logs and IDS alerts), the Windows domain (SWAGGER-DC-01, DC-02, FS-01 and CA-01), Proxmox and Docker, and UniFi. Wazuh, running in Docker on SWAGGER-NMS-01, decodes the logs, correlates them against its rules and responds, then forwards events to Splunk for search and dashboards. In the animation, a brute force attempt on SWAGGER-DC-01 raises a level 10 alert, active response blocks the source, and the alert is forwarded to Splunk." width="100%">
</picture>

<br>

<p align="center"><sub>Built and documented by <a href="https://github.com/Rayan-Aldossary">Rayan Aldossary</a></sub></p>
