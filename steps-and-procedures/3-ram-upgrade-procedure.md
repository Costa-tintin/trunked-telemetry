# 03 — RAM Inspection & Upgrade

## Before buying/reusing RAM
- Most servers need **RDIMM** (registered), not desktop-style UDIMM — check the exact part number your board supports, not just "DDR4, it'll probably work"
- Match **ECC** support — server boards expect ECC; non-ECC sticks may not even POST
- Match speed/rank where possible — mismatched sticks usually downclock to the slowest module rather than fail outright, which is a quiet performance loss, not a hard error

## Procedure
1. Power down, unplug, discharge, ESD strap on (see doc 02)
2. Locate DIMM slots — they're grouped into channels per CPU; the board silkscreen usually labels them (A1, A2, B1... or similar)
3. Open the white retention clips at both ends of the slot
4. Align the notch on the module with the notch in the slot — it only fits one way
5. Press straight down evenly at both ends until the clips snap closed on their own — if you're forcing it, the orientation is probably wrong
6. **Populate in balanced banks.** On a dual-socket board, split RAM evenly across both CPUs' channels rather than loading one CPU's slots and leaving the other empty — this keeps NUMA-aware workloads (including ESXi) running efficiently
7. Reassemble enough to power on (the cover doesn't need to go back on yet for a test boot)

## How to know it worked (verification — not just "it booted")
- Watch POST: total memory reported should match what you installed
- Check the management controller (iDRAC/iLO Lifecycle Controller diagnostics) for any memory error logged — a stick that POSTs fine can still throw correctable errors under load
- Run a proper memory test if you have any doubt: **memtest86+** from a bootable USB, or the server's built-in diagnostics if it has one — let it run at least one full pass, not just start it and look away
- From the OS once booted: `free -h` (Linux) or Task Manager/`systeminfo` (Windows) to confirm the OS sees the full amount
