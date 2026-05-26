# homelab_eos
This repository documents the infrastructure and deployment of a personal homelab designed to simulate real-world enterprise environments for troubleshooting, validation, and experimentation.

Objectives

Main goals of this homelab:

Build a real infrastructure environment
Simulate network/server incidents
Learn virtualization and containerization
Practice routing/VLAN/firewall concepts
Deploy monitoring systems
Create a reusable troubleshooting lab
Prepare future automation & cybersecurity experiments

Current Topology

Internet / ISP
      │
      ▼
MikroTik RB450G
10.10.10.1
      │
      ▼
Cisco Catalyst 2960G
(VLAN 10 Management)
      │
      ▼
Proxmox VE Host
10.10.10.10
      │
      ▼
Debian VM (docker-host)
10.10.10.20
      │
      ├── Docker Engine
      ├── Portainer
      └── Uptime Kuma

Hardware
Router
MikroTik RB450G
RouterOS v7.22.3

Managed Switch
Cisco Catalyst 2960G
Server Host
Dell XPS 13 9370
Component	Specification
CPU	Intel i7-8550U
RAM	16 GB
Storage	477 GB SSD
Network Design
Management VLAN
VLAN	Purpose
VLAN 10	Infrastructure Management
IP Addressing
Device	IP Address	Description
MikroTik	10.10.10.1	  Gateway
Proxmox	  10.10.10.10	  Hypervisor
Debian VM	10.10.10.20	  Docker Host

Subnet:

10.10.10.0/24

DNS:

1.1.1.1
8.8.8.8

Proxmox Infrastructure
Hostname
pve-01.homelab.local

Hypervisor Features
VM Virtualization
Linux Bridge Networking
VM Management
Snapshot capability
Infrastructure scaling capability

Virtual Machine
Debian Docker Host
Parameter	Value
VM ID	100
Name	docker-host
CPU	2 vCPU
RAM	4 GB
Disk	40 GB
Network	VirtIO + vmbr0
Debian Network Configuration

File:

/etc/network/interfaces

Configuration:

auto lo
iface lo inet loopback

auto ens18
iface ens18 inet static
    address 10.10.10.20/24
    gateway 10.10.10.1
    dns-nameservers 1.1.1.1 8.8.8.8

Remote Access
SSH
ssh username@10.10.10.20

Installed Base Packages
sudo
curl
wget
vim
nano
git
qemu-guest-agent
net-tools
dnsutils
tcpdump
htop
btop
unzip
ca-certificates
gnupg
lsb-release
Docker Infrastructure
Docker Engine

Verification:

docker run hello-world

Status:

Operational
Portainer
Purpose

Docker web-based management GUI.

Access
https://10.10.10.20:9443
Uptime Kuma
Purpose

Infrastructure monitoring system.

Monitors:

Ping
HTTP/HTTPS
TCP port
Latency
Uptime
Access
http://10.10.10.20:3001
Monitoring Targets

Current monitored infrastructure:

Target	  Monitor Type
MikroTik	Ping
Proxmox	  HTTPS
Debian VM	Ping

Incident Log
Duplicate IP Conflict 

Issue
Debian VM accidentally used:

10.10.10.10

which conflicted with Proxmox management IP.

Impact
Proxmox inaccessible
ARP conflict
Unstable management connectivity
Resolution

Debian VM IP changed to:

10.10.10.20
Lessons Learned
Duplicate IP detection
ARP conflict behavior
Infrastructure recovery process
Future Roadmap

Planned deployment:

WireGuard VPN
Reverse proxy (nginx)
Internal DNS (Bind9)
Grafana
Smokeping
Guacamole
Zabbix
Netshoot diagnostic containers
Multi-VLAN segmentation
Infrastructure automation
Backup strategy
Security hardening
Planned Simulation Environment

Future troubleshooting scenarios:

Port blocking
Firewall drops
DNS failures
Routing issues
VLAN mismatch
Packet loss simulation
Reverse proxy failures
SSL/TLS issues
Service outages
Latency injection

Current Infrastructure Status
Component	        Status
MikroTik	        ✅ Operational
Cisco Switch	    ✅ Operational
VLAN Management	  ✅ Operational
Proxmox	          ✅ Operational
Debian VM	        ✅ Operational
SSH Access	      ✅ Operational
Docker Engine	    ✅ Operational
Portainer	        ✅ Operational
Uptime Kuma	      ✅ Operational

Access Information
Proxmox
https://10.10.10.10:8006
Portainer
https://10.10.10.20:9443
Uptime Kuma
http://10.10.10.20:3001

Notes
Laptop lid configured to keep services running when closed
Infrastructure currently uses access VLAN 10
WireGuard deployment pending public IP assignment
Infrastructure ready for multi-VM expansion
Homelab Status

✅ Foundation established
✅ Virtualization operational
✅ Container platform operational
✅ Monitoring operational
🚀 Ready for expansion and simulation lab development
