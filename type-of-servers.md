# Types of Servers

## By physical form factor
| Type | What it is | Where you'll see it |
|---|---|---|
| Tower server | Looks like a big desktop PC, stands upright | Small office, branch site, "the server is in the cupboard" SME setups |
| Rack server (1U–4U) | Slides into a 19" rack, measured in rack units | Data centers, server rooms, ISPs |
| Blade server | Thin server module sharing power/cooling/networking with a chassis | Large data centers, high-density compute |

In Nairobi SME environments, tower and low-U rack servers dominate — full blade chassis are rare outside large enterprise/data center floors.

## By role/function
- **File server** — central storage, shared drives
- **Web server** — serves HTTP(S) (Apache, Nginx, IIS)
- **Database server** — MySQL, PostgreSQL, MSSQL, Oracle
- **Mail server** — SMTP/IMAP
- **DNS/DHCP server** — name resolution, IP assignment
- **Domain controller** — Active Directory, authentication
- **Application server** — runs the business logic layer
- **Hypervisor host** — doesn't run one role, runs many roles as VMs (this is where ESXi/Proxmox come in)
- **Print server, backup server, proxy server** — supporting roles, often combined onto one box in smaller deployments

## A pattern worth noticing
Small deployments collapse roles onto one physical box (DC + file + print on a single tower server is common locally). Larger environments split every role onto its own VM, often all hosted on a handful of physical hypervisor hosts. That's the bridge to virtualization — one physical server, many logical servers.
