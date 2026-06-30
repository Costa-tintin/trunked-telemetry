# 02 — Opening the Chassis: Tools Needed

## Before you touch anything
- Confirm the server is fully powered down (graceful shutdown, see doc 01) and unplugged from AC — both PSUs if dual
- Press the power button once after unplugging to discharge any residual standby power
- Wait about 10 seconds

## Tools
- **Phillips #2 screwdriver** — most general case screws
- **Torx driver set (T8–T15)** — some rail screws and certain rack ear/bracket fasteners use Torx, not Phillips
- **ESD wrist strap** (clip to bare metal chassis, not paint) — non-negotiable around RAM/CPU; static discharge can silently degrade components even without visible damage
- **Anti-static mat** — for anything you remove and set down (old RAM, expansion cards)
- **Needle-nose pliers** — for stubborn cable connectors or jumpers
- **Flashlight or headlamp** — server internals are dim, and you'll often be working at an angle
- **Zip ties / cable labels** — note which cable went where before disconnecting anything, especially if there isn't an obvious single routing path
- **Compressed air (canned) or an ESD-safe vacuum** — for the cleaning step
- **Isopropyl alcohol (90%+) and lint-free cloths, plus fresh thermal paste** — only needed if you're removing the CPU heatsink

## Opening it
1. Most rack servers: a single latch or button releases the top cover, which slides back and lifts off — genuinely tool-less by design
2. Tower servers: usually 1–2 thumbscrews or a side-panel latch
3. Drive bays: individual hot-swap trays usually have their own small latch — no tools needed, and technically don't even require a shutdown if the RAID is redundant (see docs 05/06 for when that matters)

## How to know you're ready to proceed
Cover off, good lighting, ESD strap on and clipped to the chassis, and a clear mental (or photographed) note of what the inside looked like before you started — that "before" photo is your fallback if you forget where a cable went.
