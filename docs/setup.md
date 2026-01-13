# Active Directory Home Lab (AD DS + DNS)

Portfolio project: Build a Windows Server Domain Controller, join a Windows 10 client, and apply basic admin tasks (OUs, Users, Groups, GPO).

## Lab Overview
- Hypervisor: VirtualBox
- VMs: Windows Server (Domain Controller), Windows 10 (Client)
- Network: NAT + Host-Only
- Domain: lab.local (example)

## Network Design
- Adapter 1: NAT (Internet)
- Adapter 2: Host-Only (Lab network)

![VirtualBox Adapters](docs/images/01-virtualbox-adapters.png)

## IP Plan (example)
- DC: 192.168.56.10/24 (DNS = 192.168.56.10)
- Win10: 192.168.56.20/24 (DNS = 192.168.56.10)

## Implementation (Screenshots)
1) DC static IP + DNS  
![DC IP/DNS](docs/images/02-dc-ip-dns.png)

2) Install AD DS + DNS  
![Roles](docs/images/03-add-roles-adds-dns.png)

3) Promote to Domain Controller + Create domain  
![Promote DC](docs/images/04-promote-dc-domain.png)

4) Configure Win10 DNS and join domain  
![Win10 DNS](docs/images/05-win10-dns-settings.png)  
![Domain Join](docs/images/06-domain-join.png)

5) Create OUs/Users/Groups  
![OUs Users Groups](docs/images/07-ou-users-groups.png)

6) Apply a basic GPO (example: disable Control Panel)  
![GPO](docs/images/08-gpo.png)

## Verification
- Ping DC from Win10
- nslookup resolves the domain
- Domain user can log in

![Verification](docs/images/09-verification.png)

## What I Learned
- DNS is critical for Active Directory
- Basic lab networking (NAT + Host-Only)
- Domain join troubleshooting basics
- Managing users/groups and applying GPO
