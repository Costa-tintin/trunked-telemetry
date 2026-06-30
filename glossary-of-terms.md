# Glossary — Server Terms

- **POST** — Power-On Self-Test; hardware checks itself before handing off to the OS
- **BIOS/UEFI** — firmware that initializes hardware and decides what to boot
- **iDRAC / iLO / IMM/XCC** — Dell / HPE / Lenovo's out-of-band remote management controllers
- **ECC RAM** — Error-Correcting Code memory; detects and fixes single-bit errors automatically
- **RDIMM / UDIMM** — Registered vs Unregistered DIMM; most servers require RDIMM, not the desktop-style UDIMM
- **NUMA** — Non-Uniform Memory Access; on multi-socket servers, each CPU has memory that's "closer" (faster) to it than memory attached to the other CPU
- **RAID** — Redundant Array of Independent Disks; combines drives for performance and/or redundancy (RAID 1 mirrors, RAID 5/6 stripe with parity, RAID 10 mirrors + stripes)
- **Hot-swap** — component (drive, fan, sometimes PSU) can be replaced while the system is running
- **Hypervisor (Type 1)** — runs directly on hardware with no host OS underneath (ESXi, Proxmox's KVM, Hyper-V in some modes)
- **VM (Virtual Machine)** — a software-defined computer running on a hypervisor, with its own virtual CPU/RAM/disk/NIC
- **vSwitch** — virtual network switch inside a hypervisor, connecting VMs to each other and to physical NICs
- **Datastore** — where a hypervisor stores VM disk files (local disk, SAN, NAS)
- **HCL (Hardware Compatibility List)** — vendor's list of hardware confirmed to work with their hypervisor; skipping this check is a common cause of failed ESXi installs on older/odd hardware
- **Out-of-band management** — managing a server through a separate dedicated channel (iDRAC/iLO) instead of through the main OS/network path
- **Graceful vs hard shutdown** — graceful = OS-initiated, services stopped in order, disks flushed; hard = power cut/forced, no cleanup
