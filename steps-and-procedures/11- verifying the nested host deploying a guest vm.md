# 11 — Verifying the Nested Host: Deploying a Guest VM

ESXi installed and reachable via the Host Client is a real result, but it's not the finish line. The actual proof a hypervisor host works is whether it can run, network, and report on a real guest VM.

## Goal
Prove the host does its actual job: license it properly, host a guest VM, give that VM network reachability, and confirm via the CLI that the host is fully operational — not just "powered on."

## Steps

### 1. Replace the evaluation license
Host Client → **Manage → Licensing**. The eval license expires in 60 days; if going the free-ESXi route, apply the free license key from the Broadcom Support Portal here instead of letting it lapse.
📸 Licensing screen before and after.

### 2. Get an OS image onto the datastore
Host Client → **Storage → [datastore] → Datastore browser → Upload**. Pick something light given limited RAM on a nested host — Alpine Linux, TinyCore, or a minimal Ubuntu Server ISO all work.
📸 Datastore browser showing the uploaded ISO.

### 3. Create/Register a VM
Host → **Create/Register VM** → New VM → select guest OS family/version → allocate modest resources (1 vCPU, 512MB–1GB RAM, 8–16GB thin-provisioned disk is plenty for a lightweight guest) → attach the uploaded ISO as the virtual CD/DVD, set it first in boot order.
📸 Each wizard step, especially the resource allocation page.

### 4. Power it on
This is the step most likely to expose the Intel-host nested-virtualization ceiling noted in doc 10. Two valid outcomes:
- **It boots** → proceed to step 5
- **It throws a power-on error** → screenshot the exact message. This is a real, reproducible platform limit, not a mistake — document it as the result, the same way a Packet Tracer gap gets called out rather than hidden.
📸 The console either way — clean boot or the error screen.

### 5. If it boots: finish the install and prove networking
Complete the lightweight OS install, get the guest an IP (it'll ride the same Host-only network as the outer ESXi VM), then ping it from the host PC.
📸 Running guest console + a successful ping.

### 6. Check Networking and Monitor regardless of step 4's outcome
- **Networking tab**: review vSwitch0 and the VM Network port group
- **Monitor tab**: CPU/memory performance graphs over the last few minutes
📸 Both tabs.

### 7. Enable SSH and confirm from the CLI
Host Client → **Actions → Services → Enable Secure Shell (SSH)**. Connect from a terminal and run a couple of read-only commands:
```
esxcli system version get
esxcli network nic list
```
📸 Terminal output.

## How to know it worked
- **Full success**: guest VM installed, networked, and pingable
- **Partial — still a valid, documentable result**: VM creation and host config all check out, but the nested power-on hits the known Intel ceiling — the licensing, storage, and networking are all still proven functional, which is most of what this exercise is actually testing
