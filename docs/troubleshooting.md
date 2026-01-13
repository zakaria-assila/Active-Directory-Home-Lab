# Troubleshooting (AD Home Lab)

This page lists the most common issues and fixes when building an AD DS + DNS lab.

---

## 1) Domain Join Fails (Most common)
### Symptoms
- "Domain could not be contacted"
- "DNS name does not exist"
- Login works locally only

### Fix
1. On Windows 10, set **DNS = DC IP** (NOT 8.8.8.8 / router DNS)
2. Verify:
   - `ipconfig /all`
   - `ping <DC-IP>`
   - `nslookup lab.local`
3. Retry domain join after DNS is correct

---

## 2) Cannot Ping DC / No Connectivity
### Symptoms
- Ping to DC fails
- Win10 cannot see the domain

### Fix
1. Ensure both VMs have:
   - Adapter 1 = NAT
   - Adapter 2 = Host-Only
2. Ensure both are on the **same Host-Only network**
3. Check IP addresses are in same subnet (example: 192.168.56.0/24)
4. Windows Firewall (lab/testing only):
   - Temporarily allow ICMP echo (ping) on DC for testing

---

## 3) DNS Issues (Name Resolution)
### Symptoms
- `nslookup lab.local` fails
- GPO does not apply
- Domain services feel slow

### Fix
1. On DC: DNS should point to itself
2. On Win10: DNS must be DC IP
3. Test:
   - `nslookup lab.local`
   - `nslookup _ldap._tcp.dc._msdcs.lab.local`
4. If needed, restart DNS service on DC

---

## 4) Time Sync / Kerberos Errors
### Symptoms
- Domain login issues
- Authentication errors after join

### Fix
- Ensure client time is close to DC time
- Commands:
  - `w32tm /query /status`
  - Sync time (as admin): `w32tm /resync`

---

## 5) GPO Not Applying
### Symptoms
- GPO created but nothing changes on client

### Fix
1. Confirm the computer/user is in the correct OU where the GPO is linked
2. Run on client:
   - `gpupdate /force`
   - `gpresult /r`
3. Reboot the client if needed

---

## 6) Wrong Network Interface Chosen
### Symptoms
- DC has internet but no lab connectivity (or opposite)

### Fix
- Re-check VirtualBox adapter order and host-only settings
- Ensure Host-Only adapter exists on host and is selected for both VMs

---

## Quick Checklist
- [ ] DC has **static IP**
- [ ] DC DNS = **DC IP**
- [ ] Win10 DNS = **DC IP**
- [ ] Both VMs share the same **Host-Only** network
- [ ] `ping DC-IP` works
- [ ] `nslookup lab.local` works
- [ ] Domain join succeeds
- [ ] `gpresult /r` shows applied policies

