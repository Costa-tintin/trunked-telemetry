# Physical Structure of a Server

## Anatomy, outside in
- **Chassis/case**: tool-less latches are standard on enterprise rack gear — top cover and drive bays usually don't need a screwdriver
- **Front panel**: power button, status LEDs (health, fan fault, drive fault — learn what each color/blink pattern means for your specific model before you need it in a hurry)
- **Drive bays**: hot-swap trays on rack servers — drives can be pulled/replaced live if running RAID with redundancy
- **Rear panel**: power supply unit(s) — often dual/redundant — NICs (one or more LAN ports + a dedicated management port), PCIe expansion slots, video/serial ports for direct console access

## Inside the case
- **Motherboard**: CPU socket(s), DIMM slots organized into channels/banks, PCIe slots, onboard NIC and storage controller chips
- **CPU socket(s)**: one (single-socket) or two (dual-socket) on most mainstream servers — on dual-socket boards, half the RAM slots are physically tied to each CPU (NUMA — more in the CPU procedure doc)
- **RAM (DIMM slots)**: arranged in channels; populating them in the wrong pattern doesn't break anything outright but kills performance (single-channel speeds instead of dual/quad)
- **Storage controller**: either a hardware RAID card (has its own cache/battery, configured in its own pre-boot menu) or a simpler HBA passing drives straight to the OS
- **Cooling**: multiple small high-RPM fans (not one big quiet one like a desktop) — loud is normal, that's why these don't sit on someone's desk
- **Riser cards**: in 1U/2U servers, PCIe cards often plug into a vertical riser instead of laying flat, to fit the low-profile case

## Why it looks the way it does
Every physical design choice traces back to one thing: serviceability without downtime. Hot-swap bays, redundant PSUs, tool-less latches, front-accessible everything — all there so a single failed component doesn't mean a full outage or even a full power-down.
