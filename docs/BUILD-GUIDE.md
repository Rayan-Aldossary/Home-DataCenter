# SWAGGER Lab Build Guide

The design reference for my home data center, one sheet per topic. Click any sheet to open it full size.

**[Download the PDF](SWAGGER-Lab-Build-Guide.pdf)** · [Back to the project](../README.md)

| # | Sheet | What it covers |
|-|-|-|
| 01 | [Project Overview](#01--project-overview) | Hostnames, general configuration, what's built, equipment list |
| 02 | [Network Topology](#02--network-topology) | Every device, every link, and the VLAN each one lives on |
| 03 | [Logical Topology](#03--logical-topology) | Layer 3 view: subnets, gateways and the inter-VLAN policy |
| 04 | [VLAN & IP Addressing](#04--vlan--ip-addressing) | Subnet plan, DHCP scopes, host and transit addresses |
| 05 | [Interfaces & Cabling](#05--interfaces--cabling) | Port-by-port mode, VLAN and what's on the other end |
| 06 | [Rack Elevation](#06--rack-elevation) | Front and rear of the 22U rack, every U and cable run |
| 07 | [Security](#07--security) | Trust zones, perimeter inspection and the hardening checklist |
| 08 | [Services & Security Configuration](#08--services--security-configuration) | STP, OSPF, DHCP, ACLs, SSH, OPNsense and Ansible |
| 09 | [Proxmox Virtual Machines](#09--proxmox-virtual-machines) | Hypervisor host and the VM roster |
| 10 | [Docker Services](#10--docker-services) | Wazuh, Splunk, LibreNMS and Portainer on NMS-01 |

## 01 · Project Overview

Hostnames, general configuration, what's built, and the full equipment list.

<a href="images/01-project-overview.png"><img src="images/01-project-overview.png" alt="Sheet 01, Project Overview: lab at a glance, hostnames and roles, general configuration, what's built, document map and equipment list" width="100%"></a>

## 02 · Network Topology

Every device, every link, and the VLAN each one lives on.

<a href="images/02-network-topology.png"><img src="images/02-network-topology.png" alt="Sheet 02, Network Topology: STC modem, ISR 4331, OPNsense firewall, core and access switches, then the VLAN 10, 20, 30, 40 and 50 zones with every connected device" width="100%"></a>

## 03 · Logical Topology

How a packet moves between subnets: the routed path, gateways and the inter-VLAN policy.

<a href="images/03-logical-topology.png"><img src="images/03-logical-topology.png" alt="Sheet 03, Logical Topology: ISR, firewall and core switch in OSPF Area 0, fanning out to five routed subnets, with the inter-VLAN routing policy table" width="100%"></a>

## 04 · VLAN & IP Addressing

Subnet plan, assignment type, gateways and every static address.

<a href="images/04-vlan-ip-addressing.png"><img src="images/04-vlan-ip-addressing.png" alt="Sheet 04, VLAN and IP Addressing: subnet plan for VLANs 10 to 50, native VLAN and transit links, plus host addressing per VLAN" width="100%"></a>

## 05 · Interfaces & Cabling

Port-by-port mode, VLAN assignment, and what's on the other end.

<a href="images/05-interfaces-cabling.png"><img src="images/05-interfaces-cabling.png" alt="Sheet 05, Interfaces and Cabling: port tables for the access switch, core switch, firewall and edge router" width="100%"></a>

## 06 · Rack Elevation

The 22U rack, front and rear, with every port numbered.

<a href="images/06-rack-elevation.png"><img src="images/06-rack-elevation.png" alt="Sheet 06, Rack Elevation: front and rear views of the 22U rack from U5 to U18, with the patch panel map and cable runs" width="100%"></a>

## 07 · Security

Trust zones, perimeter inspection, and the hardening in place.

<a href="images/07-security.png"><img src="images/07-security.png" alt="Sheet 07, Security: four trust zones from untrusted to management plane, and the hardening checklist" width="100%"></a>

## 08 · Services & Security Configuration

The configuration behind the design: spanning tree, routing, DHCP, ACLs, SSH, OPNsense and Ansible.

<a href="images/08-services-configuration.png"><img src="images/08-services-configuration.png" alt="Sheet 08, Services and Security: configuration blocks for the core switch, ISR, OPNsense, SSH and Ansible" width="100%"></a>

## 09 · Proxmox Virtual Machines

The hypervisor host and its six virtual machines.

<a href="images/09-proxmox-virtual-machines.png"><img src="images/09-proxmox-virtual-machines.png" alt="Sheet 09, Proxmox Virtual Machines: R720 host details and cards for the six VMs" width="100%"></a>

## 10 · Docker Services

The monitoring and SIEM stack on SWAGGER-NMS-01.

<a href="images/10-docker-services.png"><img src="images/10-docker-services.png" alt="Sheet 10, Docker Services: macvlan container network and the Wazuh, Splunk, LibreNMS and Portainer containers" width="100%"></a>

---

<sub>Configs shown here are sanitized. No passwords or secrets live in this repo.</sub>
