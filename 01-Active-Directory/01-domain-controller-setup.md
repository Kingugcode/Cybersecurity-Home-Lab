# Windows Server 2025 — Active Directory Domain Controller Deployment

## 1. Objective

Deploy Windows Server 2025 as a domain controller in an isolated virtual environment and establish a foundation for centralized identity and access management.

The environment will support future exercises involving domain-joined workstations, user administration, Group Policy, authentication, and security monitoring.

## 2. Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Operating System | Windows Server 2025 Evaluation |
| Hostname | DC01 |
| RAM | 4 GB |
| Virtual CPUs | 2 |
| Virtual Disk | 50 GB, dynamically allocated |
| Network | VirtualBox Internal Network |
| IPv4 Address | 192.168.10.10/24 |
| Domain | ad.cyberlab.test |
| NetBIOS Name | AD |
| Forest Functional Level | Windows Server 2025 |
| Domain Functional Level | Windows Server 2025 |

## 3. Windows Server Installation

Created a new virtual machine in Oracle VirtualBox and attached the Windows Server 2025 Evaluation ISO.

Configured the virtual hardware and installed the Desktop Experience edition to provide a graphical management environment.

After installation, signed in using the local Administrator account and opened Server Manager.

### Evidence

<img width="1917" height="1005" alt="image" src="https://github.com/user-attachments/assets/9944bf01-5a63-442f-aec3-6336376aa5a2" />


## 4. Server Configuration

Renamed the Windows Server computer to `DC01` to establish a consistent naming convention.

Verified the hostname using PowerShell:

```powershell
hostname
```

Confirmed that the server was configured with a static IPv4 address before deploying Active Directory.

### Evidence

<img width="967" height="92" alt="image" src="https://github.com/user-attachments/assets/a2574e00-2891-4003-9b5c-bb688c8de792" />


## 5. Installing Active Directory Domain Services

Opened Server Manager and navigated to:

Manage → Add Roles and Features → Active Directory Domain Services

Installed the AD DS role and launched the domain controller promotion wizard.

Selected **Add a new forest**, since this environment did not contain an existing Active Directory domain.

Configured the root domain as:

```text
ad.cyberlab.test
```

Enabled DNS Server and Global Catalog functionality, selected Windows Server 2025 functional levels, and retained the default database and SYSVOL paths.

Completed the promotion wizard and restarted the server.

### PowerShell Deployment Alternative

The Active Directory deployment wizard also generated the equivalent PowerShell configuration using:

```powershell
Install-ADDSForest
```

This demonstrated how domain controller deployment can be automated using PowerShell rather than relying exclusively on the graphical interface.

### Evidence

<img width="1035" height="778" alt="Screenshot 2026-10-25 000736" src="https://github.com/user-attachments/assets/286a1a0b-a1ec-4c81-b2c4-817612ff9f6c" />
<img width="1037" height="766" alt="Screenshot 2026-10-25 003208" src="https://github.com/user-attachments/assets/ef86a349-85c9-4359-86ca-ed623a305f91" />




## 6. Validation

The following commands are used to inspect the deployed environment:

```powershell
Get-ADDomain
Get-ADForest
```

DNS resolution was also tested:

```powershell
Resolve-DnsName DC01.ad.cyberlab.test
```

The hostname successfully resolved to the domain controller's IPv4 address:

```text
192.168.10.10
```

Further validation of domain controller health and AD-related DNS service records remains in progress.

### Evidence

<img width="972" height="617" alt="Screenshot 2026-11-10 222723" src="https://github.com/user-attachments/assets/0016f826-c5d8-4e23-933c-8acfd8d931b7" />

<img width="957" height="572" alt="Screenshot 2026-11-10 222817" src="https://github.com/user-attachments/assets/b44157b9-a939-4456-a835-7f738c70ed55" />



## 7. Technical Concepts Learned

### Domain Controller

A domain controller hosts Active Directory Domain Services and provides directory and authentication services to domain users and computers.

### Forest and Domain

A forest represents the broader Active Directory directory structure and security boundary.

A domain contains directory objects such as users, computers, and groups.

### DNS Dependency

Active Directory uses DNS to locate domain controllers and services required for authentication and domain operations.

### PowerShell Automation

The AD DS deployment wizard can generate PowerShell commands that administrators can adapt for repeatable deployments.

## 8. Challenges and Observations

- The isolated VirtualBox network initially resulted in an APIPA address because no DHCP server was available.
- Configuring a static IPv4 address provided a consistent network identity for DC01.
- The server required a restart after promotion to complete domain controller configuration.
- PowerShell documentation updates were unavailable because the VM was isolated from internet access.

## 9. Next Steps

- Complete DNS SRV record and domain controller health validation.
- Create organizational units and test user accounts.
- Configure security groups and access permissions.
- Connect a Windows client VM to the domain.
- Introduce and test Group Policy.

## 10. Outcome

Windows Server 2025 was installed and promoted to a domain controller for `ad.cyberlab.test`. The server's hostname successfully resolves through DNS.

The environment provides the foundation for further Active Directory administration and troubleshooting exercises.
