# Cloud Deployment Guide Sample — Virtual Network Appliance Deployment

## Overview

This guide explains how to deploy a virtual network appliance across cloud and virtualized environments. It covers deployment planning, image preparation, network configuration, security rules, instance creation, initial CLI configuration, WebUI access, license assignment, post-deployment verification, resizing considerations, troubleshooting, and best practices.

This sample demonstrates how cloud and hypervisor deployment documentation can be structured for enterprise networking products.

> **Note:** This is a sanitized portfolio sample. Product names, company names, support contacts, screenshots, license keys, IP addresses, image names, exact version numbers, customer details, and proprietary values have been replaced with generic examples.

---

## Audience

This guide is intended for:

- Cloud administrators
- Network administrators
- DevOps engineers
- Implementation engineers
- Technical support engineers
- Solution architects
- Technical writers documenting cloud and virtual appliance deployments

---

## Deployment Scope

This sample covers deployment on the following environments:

- Microsoft Azure-style cloud environment
- Amazon Web Services-style cloud environment
- VMware ESXi-style hypervisor environment
- Nutanix AHV / VPC-style environment
- Virtual appliance platform-style environment

---

## Deployment Use Case

In this sample scenario, a virtual network appliance is deployed to provide secure management, monitoring, and application traffic handling between users and backend services.

The deployment includes:

- One virtual network appliance
- One management interface
- One or more data interfaces
- One management subnet
- One or more application or service subnets
- Security rules for SSH, HTTPS, API, DNS, NTP, and logging
- Initial CLI configuration
- WebUI access
- License assignment
- Post-deployment validation

---

## High-level Architecture

```text
Administrators / Automation Tools
        |
        | SSH / HTTPS / REST API
        |
Management Network
        |
Virtual Network Appliance
        |
        | Application / Service Traffic
        |
Backend Application Network
```

---

## Deployment Phases

| Phase | Description |
|---|---|
| Phase 1 | Review requirements and collect network details. |
| Phase 2 | Prepare the cloud or hypervisor environment. |
| Phase 3 | Upload or select the virtual appliance image. |
| Phase 4 | Create and configure the virtual machine. |
| Phase 5 | Attach network interfaces and storage. |
| Phase 6 | Power on the appliance. |
| Phase 7 | Perform minimum initial CLI configuration. |
| Phase 8 | Enable WebUI and optional REST API access. |
| Phase 9 | Assign or import the license. |
| Phase 10 | Verify system health and network reachability. |

---

# 1. Requirements

## 1.1 Resource Requirements

The following resource values are sample recommendations. Actual sizing depends on throughput, feature usage, logging, monitoring, traffic volume, and high availability requirements.

| Deployment Size | vCPU | Memory | Storage | Use Case |
|---|---:|---:|---:|---|
| Small | 2 | 8 GB | 40 GB | Lab, proof of concept, or low-traffic deployment. |
| Medium | 4 | 16 GB | 100 GB | Standard production deployment. |
| Large | 8 | 32 GB | 250 GB | Higher traffic or multi-service deployment. |
| Custom | Based on sizing | Based on sizing | Based on sizing | Deployment requiring specific performance or interface requirements. |

---

## 1.2 Network Requirements

Collect the following information before deployment.

| Item | Example | Description |
|---|---|---|
| Management subnet | `192.0.2.0/24` | Subnet used for CLI, WebUI, and API access. |
| Data subnet | `198.51.100.0/24` | Subnet used for application or service traffic. |
| Management IP | `192.0.2.10` | IP address used to access the appliance. |
| Default gateway | `192.0.2.1` | Gateway used for outbound communication. |
| DNS server | `192.0.2.53` | DNS server for name resolution. |
| NTP server | `192.0.2.20` | NTP server for time synchronization. |
| WebUI port | `8443` | HTTPS port used for browser-based management. |
| REST API port | `9443` | Optional API access port. |

---

## 1.3 Security Rule Requirements

Configure security rules based on your organization’s security policy.

| Port | Protocol | Direction | Purpose |
|---|---|---|---|
| `22` | TCP | Inbound | SSH access to CLI. |
| `443` or `8443` | TCP | Inbound | HTTPS access to WebUI. |
| `9443` | TCP | Inbound | REST API access, if enabled. |
| `53` | TCP/UDP | Outbound | DNS resolution. |
| `123` | UDP | Outbound | NTP synchronization. |
| `514` | TCP/UDP | Outbound | Remote Syslog forwarding. |

> **Security Note:** Restrict management access to trusted administrator networks. Do not expose SSH, WebUI, or API access publicly unless approved by your security team.

---

# 2. Deployment on Microsoft Azure-style Environment

## 2.1 Azure-style Prerequisites

Before deploying the appliance, ensure that:

- You have access to the cloud portal.
- You have permission to create virtual machines, virtual networks, subnets, network interfaces, public IPs, and network security groups.
- The virtual appliance image is available.
- The target virtual network and subnet are created.
- The required ports are allowed through the network security group.
- A management IP address is planned.
- License or activation information is available, if required.

---

## 2.2 Azure-style Deployment Workflow

Use the following workflow to deploy the virtual appliance.

1. Sign in to the cloud portal.
2. Navigate to **Virtual Machines**.
3. Click **Create**.
4. Select the virtual appliance image.
5. Select the subscription and resource group.
6. Enter a virtual machine name.
7. Select the region.
8. Select the VM size.
9. Configure administrator credentials or SSH key.
10. Select the management virtual network and subnet.
11. Attach additional network interfaces, if required.
12. Configure network security group rules.
13. Review the VM configuration.
14. Click **Create**.
15. Wait until the deployment completes.
16. Open the VM console or connect through SSH.
17. Perform minimum initial configuration.
18. Enable WebUI access.
19. Import or assign the license.
20. Verify system status.

---

## 2.3 Azure-style Network Interface Planning

| Interface | Purpose | Example Subnet |
|---|---|---|
| `mgmt0` | Management, CLI, WebUI, API | `192.0.2.0/24` |
| `data0` | Client-side or ingress traffic | `198.51.100.0/24` |
| `data1` | Server-side or egress traffic | `203.0.113.0/24` |
| `ha0` | High availability heartbeat, if used | `192.0.2.128/25` |

---

## 2.4 Azure-style Post-deployment Access

After the VM is running, connect to the appliance using SSH.

```text
ssh admin@192.0.2.10
```

Expected prompt:

```text
NA>
```

Enter configuration mode:

```text
NA> enable
NA# configure terminal
NA(config)#
```

---

# 3. Deployment on Amazon Web Services-style Environment

## 3.1 AWS-style Prerequisites

Before deploying the appliance, ensure that:

- You have access to the cloud console.
- You have permission to create EC2 instances, VPCs, subnets, security groups, route tables, and network interfaces.
- The virtual appliance image or AMI is available.
- The VPC and subnets are created.
- A key pair is available for SSH access.
- Security groups allow only required management and service traffic.
- Elastic IP or private IP planning is complete, if applicable.

---

## 3.2 AWS-style Deployment Workflow

Use the following workflow to deploy the appliance.

1. Sign in to the cloud console.
2. Navigate to **Compute > Instances**.
3. Click **Launch Instance**.
4. Select the virtual appliance image or AMI.
5. Enter the instance name.
6. Select the instance type.
7. Select the key pair.
8. Select the VPC and management subnet.
9. Attach additional network interfaces, if required.
10. Configure private IP addresses.
11. Configure security groups.
12. Configure storage.
13. Review the instance configuration.
14. Click **Launch Instance**.
15. Wait until the instance state changes to **Running**.
16. Verify instance status checks.
17. Connect through SSH or console.
18. Perform minimum initial configuration.
19. Enable WebUI access.
20. Assign or import the license.
21. Verify system health.

---

## 3.3 AWS-style Security Group Example

| Rule | Protocol | Port | Source/Destination | Purpose |
|---|---|---|---|---|
| Inbound | TCP | `22` | Trusted admin subnet | SSH access. |
| Inbound | TCP | `8443` | Trusted admin subnet | WebUI access. |
| Inbound | TCP | `9443` | Trusted automation subnet | REST API access. |
| Outbound | UDP | `123` | NTP server | Time synchronization. |
| Outbound | TCP/UDP | `53` | DNS server | Name resolution. |
| Outbound | TCP/UDP | `514` | Syslog server | Log forwarding. |

---

## 3.4 AWS-style Post-deployment Access

Connect to the appliance using SSH.

```text
ssh -i appliance-key.pem admin@192.0.2.10
```

Expected prompt:

```text
NA>
```

Enter configuration mode:

```text
NA> enable
NA# configure terminal
NA(config)#
```

---

# 4. Deployment on VMware ESXi-style Environment

## 4.1 VMware-style Prerequisites

Before deploying the appliance, ensure that:

- You have administrator access to the hypervisor WebUI.
- The OVA or OVF image is available.
- A datastore with sufficient free space is available.
- A virtual network or port group is available.
- Required CPU, memory, and storage resources are available.
- Management IP address, gateway, DNS, and NTP details are planned.

---

## 4.2 VMware-style Deployment Workflow

Use the following workflow to deploy the appliance.

1. Open the hypervisor WebUI.
2. Click **Create/Register VM**.
3. Select **Deploy a virtual machine from an OVF or OVA file**.
4. Enter a unique virtual machine name.
5. Upload or select the OVA file.
6. Select the datastore.
7. Select the required network mapping.
8. Select the disk provisioning type.
9. Enable automatic power-on, if required.
10. Review the deployment settings.
11. Click **Finish**.
12. Monitor the deployment task.
13. Power on the virtual machine.
14. Open the VM console.
15. Perform minimum initial CLI configuration.
16. Enable WebUI access.
17. Assign or import the license.
18. Verify system status.

---

## 4.3 VMware-style Deployment Settings

| Setting | Example | Description |
|---|---|---|
| VM name | `network-appliance-prod` | Name of the deployed VM. |
| Image file | `network-appliance.ova` | Appliance image used for deployment. |
| Datastore | `datastore-prod-01` | Storage location for VM files. |
| Network mapping | `Management-Network` | Port group or virtual network used by the VM. |
| Disk provisioning | `Thin` or `Thick` | Storage allocation method. |
| Power on automatically | Optional | Starts VM after deployment. |

---

# 5. Deployment on Nutanix AHV-style Environment

## 5.1 Nutanix AHV-style Prerequisites

Before deploying the appliance, ensure that:

- You have administrator access to the Nutanix management UI.
- The QCOW2 image is available.
- A cluster is available for VM deployment.
- Sufficient CPU, memory, and storage are available.
- Required networks or subnets are created.
- Static IP addresses are planned, if manual assignment is used.

---

## 5.2 Nutanix AHV-style Deployment Workflow

Use the following workflow to deploy the appliance.

1. Sign in to the Nutanix management UI.
2. Navigate to **Compute & Storage > Images**.
3. Click **Add Image**.
4. Select **Image File** as the image source.
5. Upload the QCOW2 image file.
6. Set the image type to **Disk**.
7. Confirm that the image upload completes successfully.
8. Navigate to **VMs > Create VM**.
9. Enter the VM name.
10. Select the cluster.
11. Configure vCPU, cores per CPU, and memory.
12. Open the resources section.
13. Click **Attach Disk**.
14. Select **Clone from Image**.
15. Select the uploaded QCOW2 image.
16. Set the disk capacity.
17. Select the bus type.
18. Attach the required network.
19. Select the correct boot mode.
20. Review the VM configuration.
21. Save the VM.
22. Power on the VM.
23. Open the console.
24. Perform minimum initial configuration.

---

## 5.3 Nutanix AHV-style VM Configuration

| Setting | Example | Description |
|---|---|---|
| VM name | `network-appliance-ahv` | Name of the VM. |
| Image type | `Disk` | Type selected during image upload. |
| Disk operation | `Clone from Image` | Creates VM disk from uploaded image. |
| Disk size | `40 GB` | Minimum sample disk size. |
| Bus type | `SCSI` | Disk bus type. |
| Boot mode | `Legacy BIOS` | Boot mode selected for this sample. |
| Network | `Management-Subnet` | Subnet attached to the VM. |

---

# 6. Deployment on Nutanix VPC-style Environment

## 6.1 Nutanix VPC-style Prerequisites

Before deploying the appliance, ensure that:

- You have access to the central management UI.
- The QCOW2 image is uploaded or available.
- Project and cluster details are available.
- Required subnets are already configured.
- Static IP addresses are planned for each interface.
- Management, client, server, and HA subnets are identified, if applicable.

---

## 6.2 Nutanix VPC-style Deployment Workflow

Use the following workflow to deploy the appliance.

1. Sign in to the central management UI.
2. Navigate to **Compute > Images**.
3. Click **Add Image**.
4. Upload the QCOW2 image.
5. Set the image type to **Disk**.
6. Verify that the image appears in the image list.
7. Navigate to **Compute > VMs**.
8. Click **Create VM**.
9. Enter the VM name.
10. Select the project.
11. Select the cluster.
12. Configure CPU and memory.
13. Attach a disk using **Clone from Image**.
14. Select the uploaded QCOW2 image.
15. Configure disk capacity and bus type.
16. Attach the VM to the management subnet.
17. Assign a static IP address, if required.
18. Repeat subnet attachment for additional interfaces.
19. Select the required boot mode.
20. Select time zone or optional tags, if required.
21. Review all settings.
22. Save the VM.
23. Power on the VM.
24. Open the console for initial configuration.

---

## 6.3 Nutanix VPC-style Interface Planning

| Interface | Subnet | IP Assignment | Purpose |
|---|---|---|---|
| `mgmt0` | `Management-Subnet` | Static IP | CLI, WebUI, and API access. |
| `client0` | `Client-Subnet` | Static IP | Client-side traffic. |
| `server0` | `Server-Subnet` | Static IP | Backend application traffic. |
| `ha0` | `HA-Subnet` | Static IP | HA heartbeat, if configured. |

---

# 7. Deployment on Virtual Appliance Platform-style Environment

## 7.1 Platform-style Prerequisites

Before deploying a virtual appliance instance on a virtual appliance platform, ensure that:

- The host platform is configured and reachable.
- The management IP address and gateway are configured.
- WebUI access is enabled on the host platform.
- The virtual appliance image is available.
- Required licenses are available.
- Required CPU, memory, and virtual interfaces are available.
- Traffic interfaces are planned before deployment.

---

## 7.2 Platform-style Deployment Workflow

Use the following workflow to deploy the virtual appliance instance.

1. Log in to the host platform WebUI.
2. Navigate to **Virtual Appliance Management**.
3. Open the **Images** section.
4. Click **Add Image**.
5. Upload or register the virtual appliance image.
6. Enter image metadata, if required.
7. Save the image.
8. Navigate to the **Virtual Appliances** section.
9. Click **Create Virtual Appliance**.
10. Select the image.
11. Enter the instance name.
12. Select the instance size.
13. Assign CPU and memory.
14. Assign management and traffic interfaces.
15. Review the instance configuration.
16. Save the instance.
17. Start the virtual appliance instance.
18. Open the instance console.
19. Perform minimum initial configuration.
20. Assign or import the license.

---

## 7.3 Traffic Interface Planning

| Interface | Purpose | Example |
|---|---|---|
| `mgmt0` | Management access | CLI, WebUI, API |
| `port1` | Client-side traffic | Ingress traffic |
| `port2` | Server-side traffic | Egress traffic |
| `ha0` | HA heartbeat | Peer communication |

---

# 8. Minimum Initial Configuration

After deployment, configure basic system settings from the console or SSH session.

## 8.1 Enter Configuration Mode

```text
NA> enable
NA# configure terminal
NA(config)#
```

---

## 8.2 Configure Hostname

```text
NA(config)# hostname network-appliance-prod
```

---

## 8.3 Configure Management Interface

```text
NA(config)# system management interface mgmt0
```

---

## 8.4 Configure Management IP Address

```text
NA(config)# ip address mgmt0 192.0.2.10 255.255.255.0
```

---

## 8.5 Configure Default Gateway

```text
NA(config)# ip route default 192.0.2.1
```

---

## 8.6 Configure DNS

```text
NA(config)# ip nameserver 192.0.2.53
```

---

## 8.7 Configure NTP

```text
NA(config)# ntp server 192.0.2.20 4
NA(config)# ntp on
```

---

## 8.8 Configure WebUI Port

```text
NA(config)# webui port 8443
```

---

## 8.9 Enable WebUI

```text
NA(config)# webui on
```

---

## 8.10 Save Configuration

```text
NA# write memory
```

Expected result:

```text
Configuration saved successfully.
```

---

# 9. Access the WebUI

After WebUI is enabled, open a supported browser and enter:

```text
https://192.0.2.10:8443
```

Expected result:

```text
The WebUI login page appears.
```

> **Certificate Note:** If a self-signed certificate is used, the browser may display a certificate warning. Follow your organization’s certificate trust policy before proceeding.

---

# 10. License Assignment

A license may be required before the appliance can manage devices, enable features, or process production traffic.

## 10.1 License Assignment Workflow

1. Log in to the WebUI.
2. Navigate to **System > License**.
3. Click **Import License** or **Assign License**.
4. Select or paste the license key.
5. Click **Apply**.
6. Verify the license status.

---

## 10.2 CLI License Import Example

```text
NA(config)# system license <license-key>
```

> **Security Note:** Do not include real license keys in public documentation, screenshots, logs, or repositories.

---

## 10.3 Verify License Status

```text
NA# show version
```

or

```text
NA# show license
```

Expected result:

```text
License Status : Valid
Licensed Features : Enabled
Expiration Status : Active
```

---

# 11. Post-deployment Verification

Run the following checks after deployment.

## 11.1 Verify System Health

```text
NA# show system status
```

Expected result:

```text
System Health : Normal
CPU Usage     : Within expected range
Memory Usage  : Within expected range
Disk Usage    : Within expected range
```

---

## 11.2 Verify Interface Status

```text
NA# show interface
```

Expected result:

```text
Interface   Status   Link
mgmt0       up       up
port1       up       up
port2       up       up
```

---

## 11.3 Verify IP Address

```text
NA# show ip address
```

---

## 11.4 Verify Default Route

```text
NA# show ip route
```

---

## 11.5 Verify DNS

```text
NA# ping example.com
```

---

## 11.6 Verify NTP

```text
NA# show ntp
```

Expected result:

```text
NTP Service      : Enabled
Synchronization  : Synchronized
```

---

## 11.7 Verify WebUI Settings

```text
NA# show webui settings
```

---

# 12. Optional REST API Enablement

Enable REST API access only if automation or external integration is required.

## 12.1 Enable REST API

```text
NA(config)# restapi enable https 9443
```

---

## 12.2 Verify REST API Status

```text
NA# show restapi status
```

Expected result:

```text
REST API Service : Enabled
Protocol         : HTTPS
Port             : 9443
Status           : Running
```

---

# 13. Resizing Considerations

Resizing a virtual appliance may affect performance, licensing, or supportability.

## 13.1 Resizing Checklist

| Check | Description |
|---|---|
| Confirm licensed limits | Verify whether the new CPU, memory, or interface count is supported. |
| Shut down VM cleanly | Power off the VM before changing CPU, memory, disk, or NIC settings. |
| Back up configuration | Save a configuration backup before resizing. |
| Verify boot mode | Confirm the boot mode remains compatible after resizing. |
| Validate interfaces | Ensure NIC mapping and subnet assignments remain correct. |
| Recheck license | Confirm the license remains valid after resizing. |

---

## 13.2 Resizing Impact

| Scenario | Possible Impact |
|---|---|
| Reducing VM size | May remain valid but can reduce performance. |
| Increasing VM size within licensed limits | Usually acceptable after validation. |
| Increasing VM size beyond licensed limits | May require license update or reactivation. |
| Changing NIC count | May affect interface mapping and network reachability. |
| Changing boot mode | May cause boot failure if incompatible. |

---

# 14. Upgrade Planning

Before upgrading the appliance, complete the following checks:

- Review release notes.
- Confirm supported upgrade path.
- Verify system requirements.
- Verify available disk space.
- Back up the current configuration.
- Take a cloud or hypervisor snapshot, if supported.
- Confirm maintenance window.
- Notify stakeholders.
- Prepare rollback plan.

---

## 14.1 Back Up Configuration

```text
NA# write file pre_upgrade_backup
```

---

## 14.2 Upgrade Example

```text
NA(config)# system update https://updates.example.com/network-appliance.img deferred
```

> **Note:** Use only approved and trusted image sources.

---

# 15. Rollback Planning

Prepare a rollback plan before making production changes.

## Rollback Checklist

| Item | Status |
|---|---|
| Configuration backup is available. | Pending |
| Previous VM snapshot is available. | Pending |
| Previous appliance image is available. | Pending |
| Maintenance window is approved. | Pending |
| Validation checklist is ready. | Pending |
| Stakeholders are informed. | Pending |

---

## Rollback Options

Common rollback options include:

- Restore the VM snapshot.
- Restore previous configuration backup.
- Redeploy previous appliance image.
- Revert route table changes.
- Revert security rule changes.
- Disable newly enabled services.
- Reassign previous IP addresses.

---

# 16. Troubleshooting

| Issue | Possible Cause | Resolution |
|---|---|---|
| VM fails to boot | Incorrect boot mode or unsupported image format. | Verify boot mode and image compatibility. |
| VM deployment fails | Insufficient datastore, quota, or resource capacity. | Verify CPU, memory, storage, and quota availability. |
| Image is not visible | Image upload did not complete or wrong image type was selected. | Re-upload the image and set the correct image type. |
| Cannot SSH to appliance | Security rule blocks port `22` or management IP is incorrect. | Verify security rules, IP address, and routing. |
| WebUI is not reachable | WebUI service is disabled or port is blocked. | Run `show webui settings` and verify security rules. |
| REST API is unavailable | REST API service is disabled or API port is blocked. | Verify REST API status and firewall rules. |
| DNS resolution fails | DNS server is not configured or unreachable. | Run `show ip nameserver` and test DNS reachability. |
| NTP is not synchronized | NTP server is unreachable or UDP `123` is blocked. | Verify NTP server and security rules. |
| No network connectivity | NIC is attached to the wrong subnet or route is missing. | Verify NIC attachment, subnet, route table, and gateway. |
| License import fails | Invalid, expired, or mismatched license. | Verify license details and appliance identity. |
| Configuration lost after reboot | Configuration was not saved. | Run `write memory` after changes. |
| VM resizing causes license issue | New resources exceed licensed limits. | Verify licensed capacity before resizing. |

---

# 17. Best Practices

- Separate management and data traffic using different subnets or interfaces.
- Restrict management access to trusted IP ranges.
- Use SSH and HTTPS for secure access.
- Avoid exposing management ports to the public internet.
- Use strong passwords or SSH keys.
- Store credentials and license keys securely.
- Configure NTP for accurate logs and audit trails.
- Configure DNS for hostname-based communication.
- Save configuration after every validated change.
- Back up configuration before upgrades or resizing.
- Take VM snapshots before major changes.
- Validate boot mode before powering on the VM.
- Verify network interface mapping after deployment.
- Use clear naming conventions for VM, interface, subnet, and security rules.
- Do not include real IP addresses, credentials, license keys, customer names, or screenshots in public documentation.

---

# 18. Documentation Skills Demonstrated

This sample demonstrates:

- Cloud deployment guide writing
- Azure-style deployment documentation
- AWS-style deployment documentation
- VMware ESXi-style deployment documentation
- Nutanix AHV / VPC-style deployment documentation
- Virtual appliance deployment documentation
- Image upload and VM creation workflows
- Network interface and subnet planning
- Security rule documentation
- CLI-based initial configuration
- WebUI access documentation
- License assignment documentation
- Post-deployment verification
- Resizing considerations
- Upgrade and rollback planning
- Troubleshooting and best practices
- Sanitization of enterprise deployment documentation for public portfolio use
