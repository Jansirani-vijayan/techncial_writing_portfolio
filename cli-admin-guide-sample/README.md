# CLI Administrator Guide Sample — Network Management Platform

## Overview

The Command Line Interface (CLI) allows administrators to configure, manage, monitor, and troubleshoot a network management platform through text-based commands.

This sample demonstrates how CLI documentation can be structured for enterprise networking products. It includes CLI conventions, access modes, initial system configuration, network settings, WebUI access, user management, high availability, debug commands, and troubleshooting commands.

> **Note:** This is a sanitized portfolio sample. Product names, company names, contact details, IP addresses, screenshots, proprietary values, and internal command references have been replaced with generic examples.

---

## Audience

This guide is intended for:

- Network administrators
- System administrators
- Technical support engineers
- Implementation engineers
- QA engineers
- Technical writers documenting CLI-based products

---

## Documentation Scope

This sample covers:

- CLI style conventions
- CLI shortcut keys
- Access control modes
- Initial system configuration
- Basic system configuration commands
- System information display commands
- WebUI access commands
- User and password management commands
- Remote access commands
- High availability commands
- Debug and troubleshooting commands

---

# 1. CLI Basics

The CLI provides direct access to system configuration and operational commands. Administrators can use the CLI to configure management access, view system status, manage users, enable services, collect logs, and troubleshoot system issues.

---

## CLI Style Conventions

The following conventions are used throughout this guide to describe command syntax and parameters.

| Style | Description | Sample Syntax | Example |
|---|---|---|---|
| **Bold** | Indicates the CLI command keyword that must be entered exactly as shown. | `tech-report create` | `tech-report create` |
| `<parameter>` | Indicates a required parameter. Replace the placeholder with an appropriate value. | `set Address <ip_address>` | `set Address 10.40.90.10` |
| `[optional parameter]` | Indicates an optional parameter. You can include it if required. | `tech-report delete [file]` | `tech-report delete newreport` |
| `{x &#124; y &#124; ...}` | Indicates a set of required choices. You must select one option from the list. | `set NtpEnabled {yes &#124; no}` | `set NtpEnabled yes` |
| `[x &#124; y &#124; ...]` | Indicates a set of optional choices. You can select one option, or leave it blank. | `show status [address &#124; gateway &#124; subnetmask &#124; ...]` | `show status address` |

---

## Additional Notes

- Command keywords are **case-insensitive**.

  Example:

  ```text
  SET Address
  set Address
  set address
  ```

- Parameter values may be **case-sensitive**, depending on the command.

- To view command usage or available syntax, type:

  ```text
  command ?
  ```

- If a parameter value contains spaces or special characters, enclose it in double quotation marks.

  Example:

  ```text
  hostname "network appliance prod"
  ```
  ---

## 1.2 CLI Shortcut Keys

The following shortcut keys help users navigate and edit commands in the CLI.

| Shortcut | Operation |
|---|---|
| `Backspace` | Deletes the character to the left of the cursor. |
| `Up Arrow` | Displays the previous command from the current session. |
| `Down Arrow` | Displays the next command from the current session. |
| `Ctrl + A` | Moves the cursor to the beginning of the line. |
| `Ctrl + E` | Moves the cursor to the end of the line. |
| `Ctrl + F` or `Right Arrow` | Moves the cursor forward one character. |
| `Ctrl + B` or `Left Arrow` | Moves the cursor backward one character. |
| `Ctrl + D` | Deletes the character under the cursor. |
| `Ctrl + K` | Deletes text from the cursor to the end of the line. |
| `Ctrl + U` | Deletes the entire line. |

---

## 1.3 Access Control Modes

The CLI supports different access levels to control what users can view or configure.

| Mode | Prompt Example | Description |
|---|---|---|
| User Mode | `NM>` | Allows users to run basic view-only commands. |
| Enable Mode | `NM#` | Allows users to run advanced show, diagnostic, and operational commands. |
| Configuration Mode | `NM(config)#` | Allows administrators to modify system configuration. |

### Access Flow

```text
User Mode → Enable Mode → Configuration Mode
```

### Example

```text
NM> enable
NM# configure terminal
NM(config)#
```

---

# 2. Initial System Configuration

Administrators can configure the platform using the CLI or Web User Interface. During initial setup, configure management access, IP address, default route, DNS, license, and WebUI service.

---

## 2.1 Initial Configuration Workflow

Use the following workflow to complete the initial configuration.

1. Connect to the appliance console or SSH session.
2. Log in using an administrator account.
3. Enter Enable Mode.
4. Enter Configuration Mode.
5. Configure the management interface.
6. Configure the management IP address.
7. Configure the default route.
8. Configure DNS servers.
9. Configure NTP.
10. Enable WebUI access.
11. Save the configuration.

---

## 2.2 Access CLI Using SSH

Use this procedure to access the CLI using an SSH client.

### Steps

1. Open an SSH client.
2. Enter the management IP address of the appliance.
3. Select SSH as the connection type.
4. Click **Open** or connect from the terminal.
5. Enter the administrator username.
6. Enter the password.
7. Run the `enable` command to enter Enable Mode.
8. Run the `configure terminal` command to enter Configuration Mode.

### Example

```text
ssh admin@192.0.2.10
NM> enable
NM# configure terminal
NM(config)#
```

### Expected Result

The CLI prompt changes to Configuration Mode.

```text
NM(config)#
```

---

# 3. Basic System Configuration Commands

## 3.1 Configure Hostname

Use this command to configure the system hostname.

### Syntax

```text
hostname <host-name>
```

### Parameters

| Parameter | Description |
|---|---|
| `<host-name>` | Hostname assigned to the system. The value must be unique within the network. |

### Example

```text
NM(config)# hostname network-mgmt-prod
```

### Expected Result

```text
Hostname updated successfully.
```

---

## 3.2 Reset Hostname

Use this command to reset the hostname to the default value.

### Syntax

```text
no hostname
```

### Example

```text
NM(config)# no hostname
```

---

## 3.3 Display Hostname

Use this command to display the current hostname.

### Syntax

```text
show hostname
```

### Example

```text
NM# show hostname
```

### Sample Output

```text
Hostname: network-mgmt-prod
```

---

# 4. Network Configuration Commands

## 4.1 Configure Interface IP Address

Use this command to configure an IPv4 or IPv6 address on an interface.

### Syntax

```text
ip address <interface-name> <ip-address> {netmask | prefix} [overlap]
```

### Parameters

| Parameter | Description |
|---|---|
| `<interface-name>` | Name of the interface to configure. |
| `<ip-address>` | IPv4 or IPv6 address assigned to the interface. |
| `netmask` | Netmask used for IPv4 address configuration. |
| `prefix` | Prefix length used for IPv6 address configuration. |
| `[overlap]` | Optional value used when an overlapping subnet is required. |

### Example

```text
NM(config)# ip address port1 192.0.2.10 255.255.255.0
```

### Expected Result

```text
IP address configured successfully.
```

---

## 4.2 Delete Interface IP Address

Use this command to delete the IP address from a specified interface.

### Syntax

```text
no ip address <interface-name> [ip-type]
```

### Parameters

| Parameter | Description |
|---|---|
| `<interface-name>` | Name of the interface. |
| `[ip-type]` | Optional IP type. Use `4` for IPv4 or `6` for IPv6. |

### Example

```text
NM(config)# no ip address port1 4
```

---

## 4.3 Display IP Address Configuration

Use this command to display configured IP addresses.

### Syntax

```text
show ip address
```

### Example

```text
NM# show ip address
```

### Sample Output

```text
Interface   IP Address      Netmask
port1       192.0.2.10      255.255.255.0
port2       unassigned      -
```

---

## 4.4 Clear All IP Addresses

Use this command to clear all configured IP addresses.

### Syntax

```text
clear ip address
```

### Warning

Use this command carefully. Clearing IP addresses may disconnect remote management sessions.

---

# 5. Route and DNS Configuration

## 5.1 Configure Default Route

Use this command to configure the default gateway.

### Syntax

```text
ip route default <gateway-ip>
```

### Parameters

| Parameter | Description |
|---|---|
| `<gateway-ip>` | IPv4 or IPv6 address of the default gateway. |

### Example

```text
NM(config)# ip route default 192.0.2.1
```

### Expected Result

```text
Default route configured successfully.
```

---

## 5.2 Delete Default Route

Use this command to delete the configured default route.

### Syntax

```text
no ip route default <gateway-ip>
```

### Example

```text
NM(config)# no ip route default 192.0.2.1
```

---

## 5.3 Display Route Table

Use this command to display routing information.

### Syntax

```text
show ip route
```

### Sample Output

```text
Destination     Gateway       Interface
default         192.0.2.1     port1
192.0.2.0/24    connected     port1
```

---

## 5.4 Configure DNS Server

Use this command to add a DNS name server.

### Syntax

```text
ip nameserver <ip-address>
```

### Example

```text
NM(config)# ip nameserver 192.0.2.53
```

---

## 5.5 Display DNS Servers

Use this command to display configured DNS name servers.

### Syntax

```text
show ip nameserver
```

### Sample Output

```text
DNS Server 1: 192.0.2.53
DNS Server 2: 192.0.2.54
```

---

# 6. NTP Configuration

## 6.1 Configure NTP Server

Use this command to configure an NTP server.

### Syntax

```text
ntp server <ip-address> [version]
```

### Parameters

| Parameter | Description |
|---|---|
| `<ip-address>` | IP address of the NTP server. |
| `[version]` | Optional NTP version. Valid values are `1` to `4`. |

### Example

```text
NM(config)# ntp server 192.0.2.20 4
```

---

## 6.2 Enable NTP

Use this command to enable NTP time synchronization.

### Syntax

```text
ntp on [index]
```

### Parameters

| Parameter | Description |
|---|---|
| `[index]` | Optional time synchronization method. |

### Example

```text
NM(config)# ntp on
```

### Expected Result

```text
NTP service enabled successfully.
```

---

## 6.3 Disable NTP

Use this command to disable NTP.

### Syntax

```text
ntp off
```

---

## 6.4 Display NTP Status

Use this command to display NTP configuration and synchronization status.

### Syntax

```text
show ntp
```

### Sample Output

```text
NTP Service      : Enabled
Primary Server   : 192.0.2.20
Version          : 4
Synchronization  : Synchronized
```

---

# 7. System Information Display Commands

## 7.1 Show System Status

Use this command to display system resource usage.

### Syntax

```text
show system status
```

### Sample Output

```text
CPU Usage     : 18%
Memory Usage  : 42%
Disk Usage    : 35%
System Health : Normal
```

---

## 7.2 Show Version

Use this command to display software and platform version information.

### Syntax

```text
show version
```

### Sample Output

```text
Software Version : 1.0.0
Build Number     : 100
Platform         : Virtual Appliance
```

---

## 7.3 Show Interface

Use this command to display interface status and statistics.

### Syntax

```text
show interface
```

### Sample Output

```text
Interface   Status   Link   Speed
port1       up       up     1G
port2       down     down   unknown
```

---

## 7.4 Show Running Configuration

Use this command to display the current running configuration.

### Syntax

```text
show running
```

---

## 7.5 Show Startup Configuration

Use this command to display the saved startup configuration.

### Syntax

```text
show startup
```

---

# 8. CLI Output Control Commands

## 8.1 Configure Pagination

Use this command to enable paginated CLI output.

### Syntax

```text
pager <lines>
```

### Parameters

| Parameter | Description |
|---|---|
| `<lines>` | Number of lines displayed per page. |

### Example

```text
NM(config)# pager 25
```

---

## 8.2 Disable Pagination

Use this command to disable paginated CLI output.

### Syntax

```text
no pager
```

### Note

When pagination is disabled, large outputs such as full configuration or technical reports may display continuously. Use caution when running large-output commands over slow console connections.

---

## 8.3 Display Pagination Setting

Use this command to display the current pagination setting.

### Syntax

```text
show pager
```

---

# 9. WebUI Access Management Commands

## 9.1 Enable or Disable WebUI

Use this command to enable or disable WebUI access.

### Syntax

```text
webui {on | off}
```

### Examples

```text
NM(config)# webui on
NM(config)# webui off
```

---

## 9.2 Configure WebUI Port

Use this command to configure the WebUI access port.

### Syntax

```text
webui port <port>
```

### Parameters

| Parameter | Description |
|---|---|
| `<port>` | Port number used for WebUI access. |

### Example

```text
NM(config)# webui port 8443
```

---

## 9.3 Reset WebUI Port

Use this command to reset the WebUI port to the default value.

### Syntax

```text
clear webui port
```

---

## 9.4 Display WebUI Settings

Use this command to display WebUI configuration.

### Syntax

```text
show webui settings
```

### Sample Output

```text
WebUI Service : Enabled
Port          : 8443
SSL           : Enabled
```

---

# 10. Password and User Management

## 10.1 Set Enable Mode Password

Use this command to set or change the password used to enter Enable Mode.

### Syntax

```text
passwd enable [password-string]
```

### Security Note

Avoid using plain-text passwords in public examples. Use placeholders such as `<password>` in public documentation.

---

## 10.2 Change User Password

Use this command to change the password of an existing administrator account.

### Syntax

```text
passwd user <user-name> <password>
```

### Example

```text
NM(config)# passwd user admin <password>
```

---

## 10.3 Create or Update Administrator Details

Use this command to create or update administrator user information.

### Syntax

```text
user <user-name> <info>
```

### Parameters

| Parameter | Description |
|---|---|
| `<user-name>` | Administrator username. |
| `<info>` | Contact information such as email or phone number. |

### Example

```text
NM(config)# user netadmin "netadmin@example.com"
```

---

## 10.4 Delete Administrator User

Use this command to delete an administrator user.

### Syntax

```text
no user <user-name>
```

### Example

```text
NM(config)# no user testuser
```

---

## 10.5 Display Users

Use this command to display configured users.

### Syntax

```text
show users
```

### Sample Output

```text
Username    Access Level
admin       Config
operator    Enable
```

---

# 11. Configuration Management

## 11.1 Save Running Configuration

Use this command to save the current running configuration.

### Syntax

```text
write memory
```

### Example

```text
NM# write memory
```

### Expected Result

```text
Configuration saved successfully.
```

---

## 11.2 Save Configuration to Local File

Use this command to save the current configuration to a local backup file.

### Syntax

```text
write file <file-name>
```

### Example

```text
NM# write file backup_config
```

---

## 11.3 Restore Configuration from File

Use this command to restore configuration from a local backup file.

### Syntax

```text
config file <file-name>
```

### Example

```text
NM(config)# config file backup_config
```

---

## 11.4 Display Configuration Backup Files

Use this command to display saved configuration files.

### Syntax

```text
show config file [file-name] [filter]
```

---

# 12. High Availability Management Commands

## 12.1 Enable High Availability

Use this command to enable high availability.

### Syntax

```text
ha on
```

### Example

```text
NM(config)# ha on
```

---

## 12.2 Disable High Availability

Use this command to disable high availability.

### Syntax

```text
ha off [force]
```

### Parameters

| Parameter | Description |
|---|---|
| `[force]` | Forces HA disablement when the HA process is not responding. |

---

## 12.3 Configure HA Interface

Use this command to configure the interface used for HA heartbeat communication.

### Syntax

```text
ha ifname <interface-name>
```

### Example

```text
NM(config)# ha ifname port2
```

### Note

The HA interface must be configured and reachable on both peers before enabling HA.

---

## 12.4 Configure HA Peer IP

Use this command to configure the peer node IP address.

### Syntax

```text
ha peer-ip <ip-address>
```

### Example

```text
NM(config)# ha peer-ip 192.0.2.12
```

---

## 12.5 Configure HA Virtual IP

Use this command to configure the virtual IP address shared by the HA pair.

### Syntax

```text
ha vip <ip-address>
```

### Example

```text
NM(config)# ha vip 192.0.2.100
```

### Note

Ensure the virtual IP address is not used by another device on the network.

---

## 12.6 Configure HA Priority

Use this command to configure the preferred HA role.

### Syntax

```text
ha priority {master | backup}
```

### Examples

```text
NM(config)# ha priority master
NM(config)# ha priority backup
```

---

## 12.7 Display HA Configuration

Use this command to display HA configuration.

### Syntax

```text
show ha config
```

### Sample Output

```text
HA Status      : Enabled
HA Interface   : port2
Peer IP        : 192.0.2.12
Virtual IP     : 192.0.2.100
Priority       : master
Interval       : 5 seconds
```

---

# 13. Debug Commands

## 13.1 Generate System Snapshot

Use this command to collect system diagnostic data.

### Syntax

```text
debug snapshot system
```

### Description

The command generates diagnostic files that may include system activity, logs, core files, and debug information.

### Sample Output

```text
System snapshot generated successfully.
Generated files:
- system_snapshot.tar.gz
- system_logs.tar.gz
- application_core.tar.gz
```

---

## 13.2 Display Debug Files

Use this command to display available diagnostic files.

### Syntax

```text
show debug file
```

### Sample Output

```text
File                    Size        Time
system_snapshot.tar.gz  774001      2026-05-18 10:30:00
system_logs.tar.gz      424000      2026-05-18 10:31:00
```

---

## 13.3 Export Debug Files Using SCP

Use this command to export debug files to a remote SCP server.

### Syntax

```text
debug scp <username@host> [file-name]
```

### Example

```text
NM(config)# debug scp "support@192.0.2.60" system_logs
```

### Security Note

Export debug files only to trusted servers. Debug files may contain sensitive system and operational information.

---

# 14. Troubleshooting Commands

## 14.1 Test IPv4 Connectivity

Use this command to test network connectivity to an IPv4 address or hostname.

### Syntax

```text
ping <ip-address | hostname>
```

### Example

```text
NM# ping 192.0.2.1
```

---

## 14.2 Trace IPv4 Route

Use this command to trace the network path to a destination.

### Syntax

```text
traceroute <ip-address | hostname>
```

### Example

```text
NM# traceroute 192.0.2.1
```

---

## 14.3 Test IPv6 Connectivity

Use this command to test network connectivity to an IPv6 address or hostname.

### Syntax

```text
ping6 <ipv6-address | hostname>
```

### Example

```text
NM# ping6 2001:db8::1
```

---

## 14.4 Trace IPv6 Route

Use this command to trace the route to an IPv6 destination.

### Syntax

```text
traceroute6 <ipv6-address | hostname>
```

### Example

```text
NM# traceroute6 2001:db8::1
```

---

## 14.5 Configure Support Access Network

Use this command to configure the network segment allowed to access the system for support or diagnostic activities.

### Syntax

```text
support <ip-address> <netmask | prefix>
```

### Example

```text
NM(config)# support 192.0.2.0 255.255.255.0
```

### Security Note

Limit support access to trusted network segments only.

---

## 14.6 Display Support Access Settings

Use this command to display configured support access networks.

### Syntax

```text
show support
```

---

# 15. Troubleshooting Reference

| Issue | Possible Cause | Resolution |
|---|---|---|
| Cannot access CLI through SSH | Management IP, gateway, or SSH access is not configured correctly. | Verify management IP, route, and remote access settings. |
| WebUI is not reachable | WebUI service is disabled or the port is blocked. | Run `show webui settings` and verify firewall rules. |
| Hostname is not updated | Configuration was not saved. | Run `write memory` after configuration changes. |
| NTP is not synchronized | NTP server is unreachable or not configured. | Verify NTP server IP, route, and DNS settings. |
| HA does not form | HA interface, peer IP, or virtual IP is incorrect. | Verify HA settings on both peers. |
| Configuration changes are lost after reboot | Running configuration was not saved. | Run `write memory` before rebooting. |
| Debug export fails | Remote SCP server is unreachable or credentials are incorrect. | Verify server reachability and login details. |
| User cannot enter Configuration Mode | Insufficient privilege or another Config session is active. | Verify user role and active sessions. |

---

# 16. Best Practices

- Use SSH instead of Telnet for remote CLI access.
- Assign users only the access level required for their role.
- Use strong passwords and rotate credentials regularly.
- Save configuration after verifying changes.
- Configure NTP to maintain accurate system time.
- Use DNS servers for hostname-based communication.
- Validate HA configuration on both nodes before enabling HA.
- Export debug files only to trusted systems.
- Avoid exposing real IP addresses, passwords, customer names, or product-specific values in public samples.
- Use consistent command structure, examples, parameter tables, and expected results in CLI documentation.

---

# 17. Documentation Skills Demonstrated

This sample demonstrates:

- CLI administrator guide writing
- Command reference documentation
- Syntax and parameter documentation
- Initial configuration workflow writing
- Network configuration documentation
- WebUI access documentation
- User and password management documentation
- High availability documentation
- Debug and troubleshooting documentation
- Security notes and best practices
- Sanitization of enterprise product documentation for public portfolio use
