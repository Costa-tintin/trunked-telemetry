# 05 — Fan Troubleshooting

## Don't open the case first
Check the management controller (iDRAC/iLO/IPMI sensor log) before reaching for a screwdriver — it'll usually tell you exactly which fan module is flagged, by RPM or fault status, which saves a lot of guessing.

## Common symptoms → likely cause
- **Front panel fan-fault LED, system otherwise running**: one redundant fan has failed or dropped below threshold RPM — most rack servers tolerate this temporarily because fans are redundant, but it should be replaced promptly, not ignored
- **High-pitched whine or grinding**: failing bearing — replace, don't lubricate as a long-term fix
- **Thermal shutdown or throttling**: either a failed fan combined with blocked airflow, or missing blanking panels in empty drive bays (airflow takes the path of least resistance — an open bay can short-circuit the cooling path meant for the components)
- **All fans suddenly at max RPM, loud**: usually a temperature sensor reading high somewhere, not a fan problem itself — check sensor logs before assuming the fans are at fault

## Procedure
1. Identify the faulty module from the management controller log
2. Most rack servers have **hot-swap redundant fan modules** — you can often pull and replace the specific failed module while the server is running, no shutdown needed (confirm this for your specific model before relying on it)
3. If diagnosing rather than just replacing: with the server powered off and unplugged, gently spin the suspect fan by hand — resistance, grinding, or a fan that won't spin freely indicates a bearing failure
4. Check the fan's power/data connector is fully seated — a partially seated connector can look identical to a dead fan from software

## How to know it worked
RPM reading back in the normal range in the management controller, fault LED clears, and (if it had escalated that far) temperatures trend back down over the following few minutes rather than continuing to climb.
