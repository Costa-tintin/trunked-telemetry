# 08 — OS Install & Deployment Readiness

## Choosing the OS
- General-purpose roles (file/print/DC on Windows-centric networks): **Windows Server**
- Web/DNS/most open-source services: **Ubuntu Server, Rocky Linux/AlmaLinux, or Debian**
- Hypervisor host: see doc 09 — this is a different category, not a general OS

## Installation
1. Prepare install media — for enterprise servers, the cleanest method is mounting the ISO as **virtual media through the management controller** (iDRAC/iLO) over the network rather than burning a physical USB, since it works even for remote/headless installs
2. Boot from the mounted/installed media, follow the installer
3. Partition deliberately — separate partitions/volumes for OS vs. data on a server is still good practice, even though it's less emphasized than it used to be
4. Set a **static IP address** during or immediately after install — a server's IP shouldn't change on a DHCP lease renewal; anything depending on it (DNS records, firewall rules, other servers' configs) breaks silently if it does
5. Set the correct hostname and, if applicable, join it to the domain/DNS at this stage rather than later
6. **Configure NTP** (time sync) early — clock drift breaks authentication (Kerberos is especially time-sensitive), certificate validation, and makes log correlation across systems useless if timestamps don't agree
7. Apply OS updates/patches before putting anything into production
8. Enable and configure remote access (SSH for Linux, RDP for Windows) so ongoing management doesn't require physical access
9. Install the vendor management agent (Dell OpenManage, HPE management agents) so OS-level health reporting integrates with the iDRAC/iLO view

## Deployment readiness checklist (before calling it "done")
- [ ] Static IP confirmed and documented
- [ ] Hostname/DNS record correct
- [ ] NTP syncing successfully
- [ ] All OS patches applied
- [ ] Firewall rules set to least-privilege for the server's actual role
- [ ] Default credentials changed everywhere (OS, RAID controller, management controller)
- [ ] Backups configured and a restore actually tested once, not just configured
- [ ] Monitoring/alerting connected
- [ ] Restart procedure (doc 01) tested at least once in a low-stakes moment, not for the first time during an incident
- [ ] Configuration documented somewhere durable (IP, role, credentials in a password manager, not a sticky note)
