# 07 — Building/Repurposing a Server: Checklist

Whether building from raw parts or repurposing a decommissioned unit as a hypervisor host, the order of decisions matters.

## 1. Define the workload first
File server, web server, database, or hypervisor host — the answer changes everything downstream (a hypervisor host wants more RAM and cores; a file server wants storage capacity and redundancy first).

## 2. Confirm core hardware sanity
- CPU(s) present, correct, and recognized at full speed (no thermal throttling messages at POST)
- RAM populated in balanced banks, full amount recognized
- Storage drives all detected by the controller
- All fans reporting normal in the management controller
- No outstanding hardware fault logged

## 3. Storage/RAID decision
- RAID 1 (mirror) — redundancy, simplest, halves usable capacity
- RAID 5/6 — capacity-efficient with parity-based redundancy, more complex rebuild
- RAID 10 — mirrored + striped, good balance of speed and redundancy, more drives needed
- Decide and configure this in the RAID controller's own pre-boot configuration utility before installing any OS — changing RAID level after data exists usually means starting over

## 4. Network planning
- At least one NIC for data traffic; confirm the dedicated management NIC (iDRAC/iLO) is on a separate, reachable network/VLAN
- Static IP, not DHCP, for anything serving a defined role (see doc 08 for why)

## 5. BIOS/UEFI settings to check before OS install
- Boot order set correctly (USB/virtual media first during install, then internal storage)
- Virtualization extensions (Intel VT-x/EPT or AMD-V) **enabled** — required for ESXi/Proxmox, and easy to miss on older boards where it defaults off
- Date/time and NTP source if the BIOS supports it directly

## 6. Then, and only then, install the OS/hypervisor
See doc 08 (general OS) or doc 09 (ESXi specifically).
