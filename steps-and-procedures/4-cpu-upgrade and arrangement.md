# 04 — CPU Inspection & Arrangement

This is the highest-risk procedure in the set — pins bend, thermal paste application can be messed up, and a damaged socket is often not economical to fix on older server boards. Go slow.

## How CPUs are arranged
- **Single-socket boards**: one CPU, straightforward
- **Dual-socket boards**: CPU0 and CPU1, each with its own bank of RAM channels (the NUMA relationship mentioned in the RAM doc) — CPU0 usually also owns certain onboard devices (some NICs, USB controllers) on top of compute, so a board can sometimes behave oddly with CPU0 missing/faulty in ways CPU1 alone wouldn't replicate

## Procedure (inspection or reseat — same steps apply to a swap)
1. Power down, unplug, discharge, ESD strap on
2. Remove the heatsink: server heatsinks are usually held by spring-loaded screws in a **diagonal/star pattern** — loosen in that diagonal order, a little at a time on each screw, not one screw fully before the next (uneven pressure can flex the board)
3. Twist gently if the heatsink is stuck from old, hardened thermal paste — never pry with a screwdriver near the socket
4. Lift the CPU retention frame, noting the orientation (a small triangle or notch marks pin 1 / corner alignment — never insert by force, and never touch the pins or socket contacts with bare fingers)
5. If reseating the same CPU: clean off old thermal paste from both the CPU and heatsink with isopropyl alcohol and a lint-free cloth before reapplying
6. Apply a small, centered amount of fresh thermal paste (a pea-sized dot for most server CPU sizes — too much is as bad as too little, it doesn't spread evenly under pressure)
7. Reseat the CPU, close the retention frame, reinstall the heatsink, tightening screws in the same diagonal pattern, gradually, alternating sides

## How to know it worked
- POST should report the correct CPU model and core count — compare against what's printed on the chip
- Check the management controller for any CPU-related fault or thermal warning logged at boot
- Under light load shortly after boot, confirm temperatures look sane in iDRAC/iLO sensor readings rather than assuming "it posted, so the paste job was fine" — a bad paste job often won't show up until the box is under real load
