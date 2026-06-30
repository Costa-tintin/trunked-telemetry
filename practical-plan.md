# The Practical Plan

Updated: no physical server available right now, so the hands-on practical is fully virtual — VirtualBox on a regular PC, with ESXi installed nested inside it.

## What's actually happening hands-on
1. **Nested ESXi inside VirtualBox** (`steps-and-procedures/10-nested-esxi-in-virtualbox.md`) — the real practical for now. This is an unsupported-but-common learning configuration, and it has known limits (newer ESXi versions tend to PSOD in it, and on Intel host CPUs the "power on a VM inside it" step often fails). Both outcomes — full success or hitting that wall — are documented as valid results, not just the happy path.
2. **OS install fundamentals practiced on a plain VM** (`steps-and-procedures/08-os-install-and-deployment-readiness.md`) — static IP, NTP, SSH, the deployment checklist — none of this needs physical hardware, so it's fully doable now on any Linux Server VM.
3. **The restart procedure** (`steps-and-procedures/01-safe-restart-vs-hard-reset.md`) — can be rehearsed safely on a disposable VM: simulate a hung service, practice the escalation steps, no real outage risk.

## What's reference-only for now
The physical procedures — opening the chassis, RAM, CPU, fans, cleaning (`steps-and-procedures/02` through `06`) — stay in this KB because they're still useful to know and were part of the original learning goal. They're just not part of the *current* hands-on practical, since there's no physical server to apply them to yet. Revisit these the moment that changes.

## Screenshot checklist (for both LinkedIn and GitHub)
- [ ] VirtualBox VM settings — Processor tab showing Nested VT-x/AMD-V enabled
- [ ] The "Hardware Virtualization Warning" screen during ESXi install, if it appears — worth keeping even though you click through it, it's part of the honest record
- [ ] ESXi installer running inside the VirtualBox window
- [ ] DCUI screen after first boot, setting the management IP
- [ ] ESXi Host Client dashboard, logged in via browser
- [ ] Attempt to create/power on a nested VM — screenshot the result either way (success, or the error if the Intel limitation hits)

## A note on why this is still worth documenting
A failed "create a VM inside nested ESXi" attempt on an Intel host isn't a mistake to hide — it's an accurate, reproducible result of a known platform limitation. Documenting it openly (the same way Packet Tracer's gaps get called out rather than smoothed over) is more useful to anyone else trying this than pretending it just worked.
