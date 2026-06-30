# How Servers Actually Work

A server is just a computer whose job is to wait — wait for a request, do something with it, hand back a response. The difference from a laptop is around-the-clock uptime, and the room is bigger inside the case.

## The request-response loop
1. Client sends a request (HTTP, file share, DNS query, database query — whatever the service is)
2. Service software listening on a port picks it up
3. OS schedules CPU time, pulls data from RAM/storage
4. Response goes back out the NIC

## What makes server hardware different from desktop hardware
- **Uptime first**: redundant power supplies, hot-swap fans and drives, ECC RAM (corrects single-bit memory errors on the fly instead of corrupting silently)
- **Remote management**: an out-of-band controller (iDRAC on Dell, iLO on HPE, IMM/XCC on Lenovo) — a tiny separate computer on the motherboard with its own NIC, so you can power-cycle, watch sensors, and mount a virtual CD/USB even if the main OS is dead or the server is two floors away
- **Density over single-thread speed**: more cores, more RAM channels, more PCIe lanes for storage/network cards — built to serve hundreds of clients in parallel, not run one game fast
- **Multiple network interfaces**: at minimum one for normal traffic, often a separate dedicated NIC just for the management controller

## Boot sequence (the short version)
Power on → POST (hardware self-test, this is where the management controller logs hardware errors) → boot device selection (BIOS/UEFI) → bootloader → OS kernel loads → services/daemons start → server is "up" once its intended service (web, file, DB, hypervisor) is actually listening, not just powered on.

That last distinction matters for troubleshooting — "the server is on" and "the server is working" are different claims.
