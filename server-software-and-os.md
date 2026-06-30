# Server Software & Operating Systems

## Server operating systems
- **Windows Server** (2019/2022/2025) — common where Active Directory, Exchange, or Windows-only line-of-business apps are in play
- **Linux distros**: Ubuntu Server, Rocky Linux/AlmaLinux (RHEL-compatible, replaced CentOS), Debian — common for web, DNS, and most open-source services; generally lighter and free of per-seat licensing
- **Hypervisor OS** (not a general-purpose OS at all): VMware ESXi, Proxmox VE — the OS's only job is to host VMs

## Software layers on top of the OS
- **Services/daemons**: the actual workload — Apache/Nginx, MySQL/PostgreSQL, Samba/NFS, BIND (DNS), Postfix (mail)
- **Remote access**: SSH (Linux), RDP (Windows) — how you manage the box without sitting in front of it
- **Monitoring agents**: vendor tools like Dell OpenManage or HPE iLO Amalgam, plus general ones like Zabbix, Nagios, Prometheus+Grafana
- **Backup software**: Veeam, Bacula, native OS backup tools

## Key distinction worth internalizing
Out-of-band management (iDRAC/iLO) is software too — but it runs on a separate chip, with its own power and its own tiny OS, independent of whatever's installed on the main system. That's why it still answers even when the "real" OS is frozen.
