# 01 — Safe Restart vs Hard Reset (The Trick Question)

"Just restart the server" sounds like the simplest troubleshooting step there is. It's also the one most likely to make things worse if done wrong — that's the trick in it.

## Why it's a trick question
On a desktop, restarting costs you an unsaved document. On a server, an ungraceful restart can mean:
- A database mid-write gets corrupted
- A RAID array flagged as "dirty" and forced into a lengthy rebuild/consistency check on boot
- Dozens of dependent services (other servers, other VMs, client sessions) all drop at once with no warning
- Filesystem inconsistency requiring an fsck/chkdsk pass that adds significant downtime

So "restart it" is never step one. It's closer to step eight.

## The correct procedure
1. **Diagnose first.** Check the management controller (iDRAC/iLO) and OS logs for what's actually wrong. A restart that doesn't address the root cause just delays the next failure.
2. **Check who/what depends on this server.** Other services, scheduled jobs, active user sessions.
3. **Schedule a maintenance window and notify stakeholders** if this is anything beyond a personal lab box.
4. **Stop services gracefully**, in dependency order (e.g., stop the application before the database it depends on, not the other way around).
5. **Initiate a graceful OS shutdown/restart** from the OS itself (`sudo shutdown -r now` on Linux, or **Restart** from the Start menu on Windows) — not the physical power button, and not yanking power.
6. **If the OS is hung and won't respond to a graceful command**, only then escalate to a hard reset — ideally capturing a crash dump first if the OS supports it (helps diagnose why it hung in the first place).
7. **Use out-of-band management to confirm true power state** (iDRAC/iLO shows power status independent of whether the OS is responsive) rather than guessing from the front panel LED alone.
8. **On power-on, watch POST and boot logs** rather than walking away — this is where you catch a failed RAID rebuild, a missing drive, or a hung boot before it becomes a callout at 2am.
9. **Verify services come back up in the correct order** and actually confirm functionality (log in, query the database, load the web page) — power being on isn't the same as the service being up.

## How to know it worked (don't skip this)
Don't just confirm the server is pingable. Confirm the actual service responds: load the web app, run a test query, check that dependent systems reconnect. A server that's "up" but whose intended service never came back is still an outage.
