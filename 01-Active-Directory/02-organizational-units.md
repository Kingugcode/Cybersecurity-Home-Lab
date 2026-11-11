# Active Directory — Organizational Units and Validation

## Overview

After setting up my Windows Server 2025 domain controller, I wanted to make sure everything was working properly before moving on to user and group management.

I started by running a few DNS and domain controller checks, then created an organizational structure in Active Directory.

## 1. Validating the Domain Controller

I ran the following command to check DNS health:

```powershell
dcdiag /test:DNS
```

DC01 passed the DNS tests, including the domain-level DNS check.

I also verified the LDAP service record using:

```powershell
Resolve-DnsName -Type SRV _ldap._tcp.dc._msdcs.ad.cyberlab.test
```

The query returned `dc01.ad.cyberlab.test`, confirming that the domain controller was advertised through DNS.

## 2. Creating Organizational Units

Using Active Directory Users and Computers (`dsa.msc`), I created a parent OU called `CyberLab` with four child OUs:

- Users
- Groups
- Workstations
- Servers

I wanted to establish a logical structure before creating accounts, joining computers, and applying Group Policies.

<img width="752" height="525" alt="Screenshot 2026-11-10 232624" src="https://github.com/user-attachments/assets/28a9912d-859e-4bf1-a723-934e59f39c78" />


## 3. Verifying the Configuration

Rather than relying only on the graphical interface, I used PowerShell to verify the OUs:

```powershell
Get-ADOrganizationalUnit -Filter * |
Select-Object Name, DistinguishedName
```

The command returned all four child OUs under `CyberLab`.

For example:

```text
OU=Workstations,OU=CyberLab,DC=ad,DC=cyberlab,DC=test
```

<img width="908" height="607" alt="Screenshot 2026-11-10 232503" src="https://github.com/user-attachments/assets/6b164cfc-99e6-483f-b2c2-276dbb54e15a" />


This helped me understand how distinguished names identify the location of objects within Active Directory.

## 4. What I Learned

One thing that stood out was the difference between an organizational unit and a security group.

OUs are used to organize directory objects, apply Group Policy, and delegate administration. Security groups, on the other hand, are commonly used to manage permissions.

I also learned how to use PowerShell to inspect the directory structure instead of relying entirely on the GUI.

## 5. Next Steps

My next step is to create test users and security groups, configure group membership, and eventually connect a Windows client to the domain.

The goal is to understand not just how to configure these things, but also how to troubleshoot them when something goes wrong.
