# 06 — Cleaning & Physical Maintenance

Dust is a bigger problem in Nairobi's environment than in a climate-controlled data center — worth treating cleaning as routine, not an emergency response.

## Suggested cadence
Every 3–6 months for a dusty room/SME closet environment; longer intervals are fine in a properly filtered server room.

## Procedure
1. Power down gracefully, unplug, discharge, ESD strap on (docs 01–02)
2. Open the case, take a "before" photo
3. **Hold each fan still by hand while blowing compressed air through it** — letting compressed air spin the fan freely can overspin it past its rated RPM and generate back-voltage through the motor, which can damage it over repeated cleanings
4. Use a vacuum with a brush attachment (or compressed air, brief bursts) on heatsink fins, vents, and the inside of the front bezel where dust tends to cake
5. Wipe down (not the fans themselves, and nothing wet near the board) with a dry microfiber cloth where dust has compacted
6. If you're already in there and the CPU heatsink has been on for years, this is a reasonable moment to check thermal paste condition (see doc 04) — dried, cracked paste is common past the 2–3 year mark
7. Check that no cables have drooped into fan paths and that all blanking panels (empty drive bay covers, empty PCIe slot covers) are still in place — these aren't cosmetic, they maintain the airflow path
8. Reassemble, reconnect power, power on

## How to know it worked
Boot normally, then check the management controller's temperature sensors over the next 10–15 minutes under whatever normal load you can apply — temps should be flat or trending down compared to your last reading, not climbing.
