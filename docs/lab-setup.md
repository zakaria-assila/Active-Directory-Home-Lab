# Active Directory Basic Lab (VirtualBox)

## Goal
Build a small Windows enterprise lab to practice System Integration basics:
- Active Directory Domain Services (AD DS)
- DNS
- Domain join (Windows 10 client)

## Lab Setup
- Hypervisor: VirtualBox
- Network: Internal Network (labnet)
- Domain: lab.local
- Domain Controller: DC01 (Windows Server)
- Client: Windows 10 (MSEdge VM)

## IP Plan
| Machine | Role | IP | DNS |
|---|---|---|---|
| DC01 | Domain Controller + DNS | 10.0.2.10 | 10.0.2.10 |
| Win10 | Domain Client | 10.0.2.20 | 10.0.2.10 |

## What I Implemented
1. Installed AD DS and DNS on Windows Server.
2. Promoted the server to a Domain Controller (new forest: `lab.local`).
3. Created DNS Forward Lookup Zone for `lab.local` and verified records.
4. Configured internal network so DC01 and Win10 can communicate.
5. Joined Windows 10 client to the domain.

## Verification
- Connectivity test: `ping 10.0.2.10` from Win10
- DNS test: `nslookup lab.local` and `nslookup dc01.lab.local`
- Domain join confirmed in System Properties: `Domain: lab.local`

## Screenshots (Evidence)
- [ ] Ping from Win10 to DC01 (success)
- [ ] DNS Manager: Forward Lookup Zones (lab.local + _msdcs)
- [ ] “Welcome to the lab.local domain”
- [ ] Win10 System Properties showing Domain: lab.local

## Snapshots
- AD-Lab-Clean-Baseline-DC01
- AD-Lab-Clean-Baseline-Win10

## Notes / Lessons Learned
- AD relies heavily on DNS; domain join fails if DNS is not configured correctly.
- Keeping clean snapshots makes it easy to recover and iterate.
