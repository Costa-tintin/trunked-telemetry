# 10 — Nested ESXi Inside VirtualBox (the practical actually being run)

No physical server right now, so this is the real hands-on path: ESXi installed as a guest OS inside VirtualBox, on a regular PC.

## Set expectations first — this is not officially supported
Worth saying upfront, the same way a Packet Tracer gap gets called out rather than smoothed over: Broadcom/VMware doesn't support running ESXi nested inside VirtualBox (or any third-party hypervisor) for production use — it's a "works for learning, at your own risk" configuration. Two things commonly go wrong:

- **Newer ESXi (7.x/8.x) is known to throw a Purple Screen of Death (PSOD) inside VirtualBox.** ESXi 6.7 — out of VMware's mainstream support, fine for learning only, not for anything resembling production — installs far more reliably in this nested setup.
- **On Intel host CPUs, VirtualBox's nested virtualization support has a real ceiling.** A "Hardware Virtualization Warning" during the ESXi install itself is expected and safe to click through. The bigger issue shows up afterward: creating and powering on a VM *inside* the nested ESXi host often fails outright on Intel hosts, because VirtualBox doesn't fully expose a second level of nested VT-x on Intel the way it does on AMD.

Neither of those makes the exercise pointless — getting ESXi itself installed and reachable via the Host Client is still real, valid practice. Don't be surprised if "create a VM inside it" is where this breaks, and don't burn hours debugging it as if it's something done wrong.

## Setup
1. Confirm VirtualBox is current (7.x)
2. New VM: Type = Linux (Other Linux 64-bit is the typical choice for an ESXi guest); allocate at least 4GB RAM and 2 vCPUs for the outer ESXi VM, 30GB+ virtual disk
3. Settings → System → Motherboard: set **Chipset to ICH9**, untick Floppy, set the optical drive as the first boot device
4. Settings → System → Processor: tick **Enable PAE/NX** and **Enable Nested VT-x/AMD-V**
5. Settings → Network: Attached to = **Host-only Adapter**; Advanced → **Promiscuous Mode = Allow All** (needed later for a nested VM's networking to actually pass traffic)
6. Mount the ESXi ISO under Storage — ESXi 6.7 recommended specifically for this nested setup, for the reliability reason above
7. Power on, click through the Hardware Virtualization Warning if it appears, run the ESXi installer as normal

## After install
1. Reboot, set the management network IP from the DCUI (F2 at the yellow boot screen) — static IP
2. From the host PC's browser, go to `https://<esxi-ip>/` to reach the VMware Host Client
3. Attempt to create a VM inside it and power it on — this is the step most likely to expose the Intel nested-virtualization limitation

## How to know it worked (and what "partially worked" looks like here)
- **Full success**: ESXi installed, reachable via Host Client, and a nested VM powers on and boots
- **Partial success — still valid, still worth documenting**: ESXi installed and reachable via Host Client, but the nested VM fails to power on. This is the expected outcome on many Intel hosts, and the error message itself is worth screenshotting and understanding rather than treated as a dead end
- If ESXi won't install at all (repeated PSOD), that's the signal to confirm it's the 6.7 ISO and not a newer build, or to fall back to Proxmox VE for a setup that doesn't fight VirtualBox's nesting limits
