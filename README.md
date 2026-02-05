
# Active Directory Home Lab (AD DS + DNS)

Portfolio project: Build a Windows Server Domain Controller, join a Windows 11 client, and apply basic admin tasks (OUs, Users, Groups, GPO).

## Lab Overview
- Hypervisor: VirtualBox
- VMs: Windows Server (Domain Controller), Windows 11 (Client)
- Network: internal Network + NAT
- Domain: lab.local 

## Network Design
- Adapter 1: NAT (Internet)
- Adapter 2: internal Network (Lab network)

![VirtualBox Adapters](docs/images/01a-virtualbox-adapters.png)

![VirtualBox Adapters](docs/images/01b-virtualbox-adapters.png)

![VirtualBox Adapters](docs/images/01c-virtualbox-adapters.png)

![VirtualBox Adapters](docs/images/01d-virtualbox-adapters.png)
## IP Plan (example)
- DC: 192.168.56.10/24 (DNS = 192.168.56.10)
- Win10: 192.168.56.20/24 (DNS = 192.168.56.10)

## Implementation (Screenshots)
1) DC static IP + DNS  
![DC IP/DNS](docs/images/02-dc-ip-dns.png)

2) Install AD DS + DNS  
![Roles](docs/images/03-add-roles-adds-dns.png)

3) Promote to Domain Controller + Create domain  
### Promote to Domain Controller
![Deployment Configuration](docs/images/04a-deployment-configuration.png)
![Domain Controller Options](docs/images/04b-domain-controller-options.png)
![Prerequisites Check](docs/images/04d-prerequisites-check.png)

4) Configure Win11 DNS and join domain  


### 4.1 Set static IP + DNS on Win11
![Win11 IPv4 + DNS](docs/images/05a-win11-ipv4-dns.png)

### 4.2 Verify connectivity (ping + nslookup)
![Verify nslookup + ping](docs/images/05b-win11-verify-nslookup-ping.png)

### 4.3 Join Win11 to the domain
![Join domain](docs/images/05c-win11-join-domain.png)

### 4.4 Domain join success
![Welcome to the lab.local domain](docs/images/05d-win11-welcome-domain.png)

### 4.5 Login using domain credentials
![Domain login](docs/images/05e-win11-domain-login.png)

### 4.6 Post-join verification (whoami/hostname/ipconfig)
![whoami + hostname + ipconfig](docs/images/05f-win11-whoami-hostname-ipconfig.png)

### 4.7 Confirm computer account in ADUC
![ADUC computer account](docs/images/05g-aduc-win11-computer-account.png)

### 4.8 DNS records created (A record)
![DNS A record](docs/images/05h-dns-a-record-win11.png)

### 4.9 Reverse DNS (PTR record)
![DNS PTR record](docs/images/05i-dns-ptr-record-win11.png)


5) Create OUs/Users/Groups  
## 5. Create OUs / Users / Groups

### 5.1 OU Structure (Create OU_Users / OU_Computers / OU_Groups)
![OU structure](docs/06a-aduc-ou-structure.png)

### 5.2 Move WIN11 computer object to OU_Computers
![Move WIN11 to OU_Computers](docs/06b-aduc-move-win11-to-ou-computers.png)

### 5.3 Create domain user (labuser) in OU_Users
![Create user labuser](docs/06c-aduc-create-user-labuser.png)

### 5.4 Create security group (GG_IT_Admins) in OU_Groups
![Create group GG_IT_Admins](docs/06d-aduc-create-group-gg_it_admins.png)

### 5.5 Add labuser to GG_IT_Admins group
![Add labuser to GG_IT_Admins](docs/06e-gg_it_admins-adds-member-labuser.png)

### 5.6 Log in to WIN11 using the domain user (LAB\labuser)
![Win11 login labuser](docs/06f-win11-login-labuser.png)

### 5.7 Verify identity on WIN11 (whoami)
![whoami labuser](docs/06g-win11-whoami-labuser.png)


6) Apply a basic GPO (example: disable Control Panel)  
![GPO](docs/images/08-gpo.png)

## Verification
- Ping DC from Win11
- nslookup resolves the domain
- Domain user can log in

![Verification](docs/images/09-verification.png)

## What I Learned
- DNS is critical for Active Directory
- Basic lab networking (NAT + Host-Only)
- Domain join troubleshooting basics
- Managing users/groups and applying GPO
