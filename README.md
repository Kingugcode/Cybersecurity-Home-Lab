# Cybersecurity & Systems Administration Home Lab

## Project Overview

This home lab is designed to develop hands-on skills in Windows Server administration, Active Directory, networking, virtualization, troubleshooting, and security monitoring.

The project uses Oracle VirtualBox to simulate an enterprise IT environment.

## Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Server OS | Windows Server 2025 Evaluation |
| Domain Controller | DC01 |
| Active Directory Domain | ad.cyberlab.test |
| DC01 IPv4 Address | 192.168.10.10/24 |
| Network | Isolated VirtualBox Internal Network |
| DNS | Hosted on DC01 |

## Progress

- [x] Created Windows Server 2025 VM
- [x] Configured a static IPv4 address
- [x] Installed Active Directory Domain Services
- [x] Promoted DC01 to a domain controller
- [ ] Complete domain controller and DNS health validation
- [ ] Create organizational units, users, and groups
- [ ] Join a Windows client to the domain
- [ ] Configure and test Group Policy
- [ ] Perform networking and authentication troubleshooting
- [ ] Integrate a SIEM for security monitoring

## Skills Being Developed

- Windows Server administration
- Active Directory and DNS
- PowerShell administration
- TCP/IP networking
- Virtualization
- Security monitoring and incident investigation

## Documentation

Each completed lab will include the objective, configuration steps, validation commands, results, and troubleshooting notes.

All work is performed in an isolated test environment.
