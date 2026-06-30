# trunked-telemetry
# Trunked Telemetry — Servers KB

Hands-on notes and procedures from learning server hardware, server software, and virtualization, as part of the infrastructure track alongside CCNA. Written learner-to-learner — not a vendor manual, just what I found out and verified myself, including the parts that didn't work as expected.

## Why this exists
Most networking content stops at switches and routers. But every network exists to get traffic to and from a server. Understanding what's on the other end — the box itself, how it boots, what's swappable, how it's virtualized — closes that gap.

## Current status
No physical server on hand right now, so the active hands-on practical runs fully virtual: **ESXi 6.7 installed nested inside VirtualBox**, on a regular PC. That install is up and running — see `steps-and-procedures/10` and `11` for the setup and the verification practical (licensing, guest VM deployment, networking, CLI checks).

The hardware-focused procedures (opening a chassis, RAM, CPU, fans, cleaning) are documented as reference material for when physical access is available — common brands seen on the Kenyan secondhand enterprise market are Dell PowerEdge, HPE ProLiant, and Lenovo/IBM System x, since most SMEs here run on retired enterprise gear rather than new boxes.

## Structure
- **Top-level files** — concepts: how servers work, types of servers, server software/OS, common market hardware, physical anatomy, glossary, and the practical plan
- **`steps-and-procedures/`** — numbered, hands-on procedures in the order they're meant to be followed, each with tools/access needed and a "how to know it worked" verification step

### Top-level concept docs
| File | Covers |
|---|---|
| `how-servers-work.md` | Request-response loop, what makes server hardware different, boot sequence |
| `types-of-servers.md` | Tower/rack/blade form factors, server roles (file, web, DB, hypervisor, etc.) |
| `server-software-and-os.md` | Windows Server, Linux distros, hypervisor OSes, service/monitoring/backup software |
| `common-market-servers.md` | Dell PowerEdge, HPE ProLiant, Lenovo ThinkSystem — new, refurbished, white-box, and cloud |
| `physical-structure.md` | Chassis anatomy, motherboard, RAM channels, storage controllers, cooling, riser cards |
| `glossary-of-terms.md` | POST, BIOS/UEFI, iDRAC/iLO, ECC, RDIMM, NUMA, RAID, hypervisor, vSwitch, datastore, HCL |
| `practical-plan.md` | The actual hands-on plan given current hardware access, plus the screenshot checklist |

### Procedures (`steps-and-procedures/`)
| # | File | Status |
|---|---|---|
| 01 | Safe restart vs. hard reset | Practiced on disposable VMs |
| 02 | Opening the chassis — tools needed | Reference (needs physical hardware) |
| 03 | RAM inspection & upgrade | Reference |
| 04 | CPU inspection & arrangement | Reference |
| 05 | Fan troubleshooting | Reference |
| 06 | Cleaning & physical maintenance | Reference |
| 07 | Build/repurpose a server — checklist | Conceptual, applies either way |
| 08 | OS install & deployment readiness | Active — done on VMs |
| 09 | ESXi install & configure (bare-metal) | Reference, for when hardware is available |
| 10 | **Nested ESXi inside VirtualBox** | **Active — done, ESXi 6.7 running** |
| 11 | **Verifying the nested host: deploying a guest VM** | **Active — current step** |

## A note on documenting limits, not just wins
Nested ESXi inside VirtualBox isn't officially supported by Broadcom/VMware, and on Intel host CPUs the "power on a VM inside it" step often hits a real platform ceiling. That's documented openly in doc 10/11 rather than smoothed over — a failed step that's a known, reproducible limitation is still useful information, the same way Packet Tracer's protocol gaps get called out directly in other parts of this content rather than glossed over.

## Related repos
- [`root-cause`](https://github.com/Costa-tintin/root-cause) — IT support troubleshooting KB (hardware, networking, OS, server issue categories)
- [`networking-labs`](https://github.com/Costa-tintin/networking-labs) — CCNA-aligned networking labs and configs
