<p align="center">
  <img src="banner.svg" alt="Home Data Center: a 22U rack with a Cisco ISR 4331, OPNsense on a CloudGenix ION 3000, two Catalyst 3850 switches, a UniFi UNAS Pro and a Dell PowerEdge R720" width="100%">
</p>

<p align="center">
  <img alt="Cisco IOS XE" src="https://img.shields.io/badge/Cisco-IOS%20XE-049FD9?style=flat-square&logo=cisco&logoColor=white&labelColor=1D1D1D">
  <img alt="OPNsense" src="https://img.shields.io/badge/OPNsense-firewall%20%26%20IDS-D94F00?style=flat-square&logo=opnsense&logoColor=white&labelColor=1D1D1D">
  <img alt="Proxmox VE" src="https://img.shields.io/badge/Proxmox-VE-E57000?style=flat-square&logo=proxmox&logoColor=white&labelColor=1D1D1D">
  <img alt="Windows Server 2022" src="https://img.shields.io/badge/Windows%20Server-2022-0078D4?style=flat-square&labelColor=1D1D1D">
  <img alt="Docker" src="https://img.shields.io/badge/Docker-LibreNMS-2496ED?style=flat-square&logo=docker&logoColor=white&labelColor=1D1D1D">
  <img alt="UniFi" src="https://img.shields.io/badge/UniFi-storage%20%26%20Protect-006FFF?style=flat-square&logo=ubiquiti&logoColor=white&labelColor=1D1D1D">
  <br>
  <img alt="CCNA certified" src="https://img.shields.io/badge/CCNA-certified-1BA0D7?style=flat-square&logo=cisco&logoColor=white&labelColor=1D1D1D">
  <img alt="Security+ in progress" src="https://img.shields.io/badge/Security%2B-in%20progress-C8202F?style=flat-square&labelColor=1D1D1D">
</p>

A small company network, built at home on the same hardware businesses run: Cisco routing and switching, an OPNsense firewall, a Proxmox virtualization host, a Windows Server domain, UniFi storage and surveillance, and a monitoring stack.

## Topology

```mermaid
flowchart TB
    isp(["STC fiber<br/>Internet"])
    rtr["<b>Cisco ISR 4331</b><br/>Edge router, NAT"]
    fw["<b>OPNsense</b><br/>CloudGenix ION 3000<br/>Firewall and IDS"]
    core["<b>Catalyst 3850, core</b><br/>Layer 3, inter-VLAN routing<br/>DHCP relay, guest DHCP"]
    acc["<b>Catalyst 3850, access</b><br/>Layer 2, 48 ports"]
    nas["<b>UniFi UNAS Pro</b><br/>7-bay storage<br/>Backups, camera footage"]
    cams["<b>UniFi Protect cameras</b><br/>Surveillance"]
    ap["<b>UniFi access points</b><br/>Internal and Guest Wi-Fi"]
    admin["<b>Admin workstation</b><br/>Management VLAN"]

    subgraph pve["Dell PowerEdge R720, Proxmox VE"]
        dc1["<b>SWAGGER-DC-01</b><br/>AD DS, DNS, DHCP"]
        dc2["<b>SWAGGER-DC-02</b><br/>AD DS, DNS"]
        fs1["<b>SWAGGER-FS-01</b><br/>Files, WSUS"]
        ca1["<b>SWAGGER-CA-01</b><br/>PKI, NPS"]
        dock["<b>Docker host</b><br/>LibreNMS"]
        dc1 ~~~ dc2
        fs1 ~~~ ca1
    end

    isp --> rtr
    rtr --> fw
    fw --> core
    core ==>|"2 × 10G EtherChannel"| acc
    acc --> pve
    acc --> nas
    acc --> cams
    acc --> ap
    acc --> admin

    classDef gear fill:#1D1D1D,stroke:#9AA1AA,color:#E9EBEE
    classDef edge fill:#2A2D31,stroke:#6C727B,color:#E9EBEE
    class rtr,fw,core,acc,nas,cams,ap,admin,dc1,dc2,fs1,ca1,dock gear
    class isp edge
    style pve fill:#2A2D31,stroke:#6C727B,color:#E9EBEE
```

The ISR 4331 handles the internet connection and NAT. OPNsense sits behind it as the firewall and IDS without a second layer of NAT, and the core switch routes between VLANs.

## Hardware

| Device | Role |
|---|---|
| Cisco ISR 4331 | Edge router, NAT, WAN |
| CloudGenix ION 3000 | OPNsense firewall and IDS between the edge router and the core |
| Cisco Catalyst 3850-48 | Core switch: layer 3, inter-VLAN routing, DHCP relay |
| Cisco Catalyst 3850-48 | Access switch: layer 2, 2 × 10G EtherChannel to the core |
| Dell PowerEdge R720 | Proxmox VE host, 384 GB RAM |
| UniFi UNAS Pro | 7-bay storage for backups, files and camera footage |
| UniFi Protect cameras | Surveillance |
| UniFi access points | Internal and Guest Wi-Fi |
| UniFi UPS and rack PDU | Power |

<details>
<summary><b>Rack elevation (22U)</b></summary>

| U | Device |
|---|---|
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

| VLAN | Name | Subnet | Gateway | Addressing |
|---|---|---|---|---|
| 10 | Management | 192.168.10.0/24 | 192.168.10.254 | Static |
| 20 | Internal | 192.168.20.0/24 | 192.168.20.254 | DHCP from SWAGGER-DC-01, relayed by the core |
| 30 | Guest | 192.168.30.0/24 | 192.168.30.254 | DHCP from the core switch |
| 40 | Servers | 192.168.40.0/24 | 192.168.40.254 | Static |
| 999 | Native | None | None | No hosts |

Gateways are the last usable address in each subnet and live on the core switch. The Proxmox host uses two links: one access port in the Management VLAN for the host itself, and one trunk carrying VLANs 20 and 40 for the virtual machines.

## Servers

Active Directory domain: `swagger.lab`

| Host | Services | Address |
|---|---|---|
| SWAGGER-DC-01 | AD DS, DNS, DHCP, NTP | 192.168.40.1 |
| SWAGGER-DC-02 | Second domain controller: AD DS, DNS | 192.168.40.2 |
| SWAGGER-FS-01 | File server, WSUS | 192.168.40.3 |
| SWAGGER-CA-01 | Certificate authority, NPS (RADIUS) | 192.168.40.4 |
| SWAGGER-WKS-01 | Windows 11 domain client | DHCP, VLAN 20 |
| Docker host | LibreNMS and security monitoring | VLAN 40 |

## Security design

- **Segmentation.** Management, users, guests and servers each get their own VLAN. The native VLAN carries no hosts.
- **Firewall and IDS.** OPNsense filters and inspects traffic between the edge router and the core.
- **Guest isolation.** The Guest VLAN gets internet access only, with its own DHCP on the core switch.
- **No inbound exposure.** No port forwards, no VPN and no public services.
- **Identity.** Active Directory with two domain controllers, plus a certificate authority and NPS for RADIUS.
- **Patching.** WSUS manages Windows updates across the domain.
- **Monitoring.** LibreNMS watches every device over SNMP, alongside security monitoring tools on Docker.
- **Surveillance.** UniFi Protect cameras, with footage kept on the UNAS Pro.
- **Backups.** Servers and files back up to the UNAS Pro, separate from the R720's own drives.
- **Safe publishing.** Configs are sanitized before they're committed. No passwords or secrets live in this repo.

---

<p align="center"><sub>Built and documented by <a href="https://github.com/Rayan-Aldossary">Rayan Aldossary</a>, CCNA</sub></p>
