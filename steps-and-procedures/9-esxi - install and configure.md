# 09 — ESXi Install & Configure (Bare-Metal — Reference for When Hardware Is Available)

> No physical server on hand right now — see `10-nested-esxi-in-virtualbox.md` for the practical actually being run. Keeping this doc for when real hardware is available, since the steps differ in a few places (notably licensing and HCL checks that don't apply to a nested/virtual install).

## Before downloading anything
Check your server's CPU against **VMware's Hardware Compatibility List (HCL)** — this is one of the biggest reasons ESXi installs fail or behave oddly on older/odd hardware. Confirm in BIOS that **Intel VT-x and EPT** (or AMD-V/RVI) are enabled — without this, ESXi won't install at all.

## Licensing — worth checking at install time, not assuming
VMware/Broadcom's free ESXi availability has changed more than once since the Broadcom acquisition: it was discontinued for new users in early 2024, then a free edition of ESXi 8.0 Update 3e returned in 2025, downloadable from the Broadcom Support Portal with an embedded free license key — for non-production/home-lab use, no vCenter connectivity, no Broadcom support included. Given how often this has shifted, check the current terms on Broadcom's site at install time rather than relying on this note. Proxmox VE remains a fully free, full-featured alternative if licensing friction gets in the way.

## Install procedure
1. Download the ESXi installer ISO (free edition, if using it) from the Broadcom Support Portal — requires registering an account
2. Mount the ISO as virtual media through iDRAC/iLO (or burn to USB if working locally without remote management access)
3. Boot the server from the mounted media
4. Follow the ESXi installer: accept the EULA, select the install disk (a small dedicated boot drive or SD/internal USB module if your server has one — keeps the install separate from VM storage), set the root password
5. Reboot — ESXi boots directly as the hypervisor, no separate OS underneath
6. Set the management network IP (static, per doc 08's reasoning) from the **Direct Console User Interface (DCUI)** on first boot — press F2 at the yellow ESXi boot screen
7. From another machine on the same network, browse to `https://<esxi-ip>/` — this opens the **VMware Host Client**, log in as root

## Basic configuration in the Host Client
- **Storage**: confirm the datastore (local disk presented by the RAID controller) is recognized
- **Networking**: review the default vSwitch — add port groups/VLANs as needed if your network is segmented
- **Create a VM**: New VM → choose guest OS type → allocate vCPU/RAM/disk from the host's resources → mount an OS ISO (uploaded to the datastore or via virtual media) → install a guest OS to prove the host actually works end-to-end

## How to know it worked
Not just "ESXi installed." Create at least one VM, install a guest OS in it, and confirm it boots and gets network connectivity — that's the real proof the host, storage, and networking are all correctly configured, not just that the hypervisor itself is running.
