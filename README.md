# Cybersecurity & Systems Administration Home Lab

## Project Overview

I'm building this home lab to develop practical skills in Windows Server administration, Active Directory, networking, virtualization, troubleshooting, and security operations.

The goal is to move beyond theoretical knowledge by configuring systems, testing how they communicate, deliberately introducing faults, and investigating problems in a controlled environment.

The lab is built using Oracle VirtualBox on my personal computer.

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

## Project Progress

- [x] Installed and configured Windows Server 2025
- [x] Configured static IPv4 addressing
- [x] Installed Active Directory Domain Services
- [x] Promoted DC01 to a domain controller
- [x] Verified hostname resolution using DNS
- [ ] Complete domain controller health validation
- [ ] Create organizational units, users, and security groups
- [ ] Join a Windows client to the domain
- [ ] Configure Group Policy
- [ ] Perform network and authentication troubleshooting
- [ ] Integrate a SIEM and investigate security events

## Project Documentation

### 01 — Active Directory

Windows Server deployment, AD DS configuration, domain creation, identity management, and Group Policy.

[View Active Directory Documentation](01-Active-Directory/01-domain-controller-setup.md)

### 02 — Networking

Static IPv4 configuration, DNS validation, network isolation, and troubleshooting exercises.

[View Networking Documentation](02-Networking/01-network-baseline.md)

## Skills Being Developed

- Windows Server administration
- Active Directory Domain Services
- DNS and TCP/IP networking
- PowerShell administration
- Virtualization and infrastructure troubleshooting
- Security monitoring and incident investigation

## Next Steps

Expand the environment with a Windows client VM, configure centralized identity management, and introduce security monitoring through a SIEM.

This repository will be updated as I complete additional exercises and document troubleshooting findings.
