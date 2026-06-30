# Servers Commonly Seen in the Market (Kenya/East Africa Context)

## New, enterprise-grade
- **Dell PowerEdge** (R-series rack: R440, R640, R740, R750; T-series tower: T140, T340) — probably the most common brand in East African enterprise IT
- **HPE ProLiant** (DL360, DL380, ML110, ML350) — close second, strong local reseller/support presence
- **Lenovo ThinkSystem** (formerly IBM System x)

## Refurbished/used market (very common locally)
A large share of "first server" experience here comes from refurbished units — Dell PowerEdge R720/R730 and HPE ProLiant DL380 Gen8/Gen9 are everywhere on the secondhand market at a fraction of new price, because large enterprises and data centers cycle hardware out every 3–5 years. These are perfectly capable for learning, homelabs, and even light production use, with the trade-off being out-of-warranty parts and higher power draw than current-gen equivalents.

## White-box / SME-built
Smaller businesses sometimes run a regular desktop-class PC or a basic tower as "the server" rather than true enterprise hardware — works for very small file/print sharing, but lacks ECC RAM, redundant PSU, and remote management, so it's a single point of failure with no early-warning system.

## Cloud (not physical, but worth naming)
AWS EC2, Azure VMs, Google Cloud Compute Engine — "servers" that are just slices of someone else's data center, billed by usage. Worth knowing the contrast: a physical server you can put your hands on vs. a virtual instance you can only reach through an API/console.
