# ESXi basic commands

### ESXCLI Command Syntax

The ESXCLI commands follow a hierarchical structure:
`esxcli [options] {namespace} + {command} [command_options]`

### ESXCLI Available Namespaces
| Namespace | Description |
| :--- | :--- |
| `esxcli` | Commands related to the ESXCLI system itself for getting version info or listing commands. |
| `device` | Commands for device management, often used to list and manage physical devices. |
| `fcoe` | Commands for managing Fibre Channel over Ethernet configuration. |
| `graphics` | Commands for managing VMware graphics devices and properties. |
| `hardware` | Commands for viewing and configuring VMkernel hardware properties. |
| `iscsi` | Commands for configuring and managing VMware iSCSI storage adapters. |
| `licensing` | Operations to manage the host's licensing credentials. |
| `network` | The most comprehensive namespace, covering all aspects of host networking. |
| `nvme` | Commands for managing the NVMe driver and devices. |
| `rdma` | Operations pertaining to Remote Direct Memory Access (RDMA) protocol stack. |
| `sched` | Commands for managing VMkernel scheduling related functions. |
| `software` | Commands for managing the ESXi software image and packages (VIBs). |
| `storage` | Commands for managing storage components and file systems. |
| `system` | Commands for configuring core VMkernel system properties and related services. |
| `vm` | A small number of operations for Virtual Machine control. |
| `vsan` | Commands for managing the vSAN (Virtual SAN) environment. |





### Some of the commonly used commands

| Namespace | Command | Description |
| :--- | :--- | :--- |
| **Core Services** | | |
| `/etc/init.d/hostd` | `start, stop, restart, status` | Controls the core **Host Daemon**. `restart` is the primary fix for local management issues. |
| `/etc/init.d/vpxa` | `start, stop, restart, status` | Controls the **vCenter Agent**. `restart` is the primary fix for "Host Not Responding" errors in vCenter. |
| `/etc/init.d/SSH` | `start, stop, restart, status` | Controls the **Secure Shell (SSH)** service for remote access. |
| `/sbin/chkconfig` | `--list` | Lists all recognized system services and their permanent auto-start status. |
| **Host System & Configuration** | | |
| `esxcli system maintenanceMode` | `set --enable {true, false}` | Puts the host into or takes it out of Maintenance Mode. |
| `esxcli system shutdown` | `reboot, poweroff` | Triggers a host shutdown or reboot. Requires `-d <seconds>` and `-r <reason>`. |
| `esxcli system version` | `get` | Retrieves the host's version, build number, and update level. |
| `esxcli system hostname` | `get` | Retrieves the host's current hostname, domain, and FQDN. |
| `esxcli system ssh` | `client, server, key, version` | Views (`get`) or permanently configures (`set`) the SSH service auto-start policy. |
| `esxcli system account` | `list, add, remove, set` | Manages local ESXi user accounts (listing, creating, deleting, and modifying). |
| **Networking** | | |
| `esxcli network nic` | `list` | Lists all physical network adapters (vmnics) installed on the host. |
| `esxcli network nic` | `get -n <vmnic_name>` | Gets detailed information (driver, firmware, speed) about a specific NIC. |
| `esxcli network vswitch standard` | `list` | Lists all standard virtual switches (vSwitches) and their uplinks/port groups. |
| `esxcli network ip interface` | `list` | Lists all VMkernel network interfaces (vmk) and their assigned services (vMotion, Management). |
| `esxcli network ip interface ipv4` | `get` | Displays the IPv4 configuration (IP, netmask) for all VMkernel interfaces. |
| `esxcli network firewall` | `get, set --enabled {true, false}` | Views (`get`) or enables/disables (`set`) the ESXi firewall. |
| **Storage** | | |
| `esxcli storage core adapter` | `list` | Lists all Storage Host Bus Adapters (HBAs) on the system (e.g., `vmhba0`). |
| `esxcli storage core device` | `list` | Lists all storage devices (LUNs/disks) visible to the host (by NAA ID). |
| `esxcli storage core adapter` | `rescan --all` | Scans all storage adapters for new devices or path changes. **Crucial.** |
| `esxcli storage filesystem` | `list` | Lists all mounted filesystems (datastores), showing name, type (VMFS/NFS), and path. |
| `esxcli storage nfs` | `list, add, remove` | Manages NFS volume connections (listing, mounting, and unmounting). |
| **Virtual Machine (VM) Control** | | |
| `esxcli vm process` | `list` | Lists all running VMs and their crucial **World ID** (process identifier). |
| `esxcli vm process` | `kill -w <WorldID> -t {soft, hard, force}` | Used to terminate an unresponsive VM process using its World ID. (`force` is the last resort). |
| **Hardware** | | |
| `esxcli hardware cpu` | `list` | Displays detailed information about each logical processor (CPU core) on the host. |
| `esxcli hardware memory` | `get` | Displays the total physical memory installed and its current usage statistics. |
| `esxcli hardware platform` | `get` | Retrieves hardware information like the system UUID, manufacturer, and model (BIOS details). |
| `esxcli hardware clock` | `get` | Displays the current hardware clock time. |