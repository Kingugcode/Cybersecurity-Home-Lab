# Network Configuration and DNS Validation

## 1. Objective

Configure a static IPv4 address for DC01 and validate DNS name resolution within an isolated VirtualBox network.

This exercise focuses on IP addressing, network isolation, DNS configuration, and foundational troubleshooting.

## 2. Network Configuration

| Setting | Value |
|---|---|
| Server | DC01 |
| Network Adapter | Ethernet |
| Network Type | VirtualBox Internal Network |
| IPv4 Address | 192.168.10.10 |
| Prefix Length | /24 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | Not configured |
| DNS | Local DC01 DNS service |

## 3. Initial Network Investigation

After installing Windows Server, inspected the available network adapters and IP configuration.

```powershell
Get-NetAdapter
Get-NetIPAddress -AddressFamily IPv4
```

The server initially had the APIPA address:

```text
169.254.251.47
```

This occurred because the isolated network did not have a DHCP server assigning addresses.

## 4. Static IPv4 Configuration

Assigned a static address using PowerShell:

```powershell
New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 192.168.10.10 -PrefixLength 24
```

Configured the DNS client to use DC01:

```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 192.168.10.10
```

After domain controller promotion, the DNS client configuration was also observed using the local loopback address `127.0.0.1`, which refers to the same server.

## 5. Configuration Verification

Verified the IPv4 configuration:

```powershell
Get-NetIPAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
```

The output confirmed:

- IPv4 address: 192.168.10.10
- Prefix length: 24
- Assignment origin: Manual
- Address state: Preferred

Checked DNS client configuration:

```powershell
Get-DnsClientServerAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
```

## 6. DNS Resolution Test

Executed:

```powershell
Resolve-DnsName DC01.ad.cyberlab.test
```

The query returned an A record pointing to:

```text
192.168.10.10
```

An IPv6 AAAA record was also returned.

This confirmed successful hostname resolution within the lab.

### Evidence

*Insert screenshots of the static IP configuration, DNS client settings, and successful DNS lookup.*

## 7. Technical Concepts Learned

### Static IP Addressing

A static IPv4 address provides a consistent address for servers and services that other systems depend on.

### APIPA

Automatic Private IP Addressing assigns an address in the `169.254.0.0/16` range when a DHCP-configured interface cannot obtain a lease.

### DNS A Records

An A record associates a hostname with an IPv4 address.

### DNS AAAA Records

An AAAA record associates a hostname with an IPv6 address.

### Loopback Address

`127.0.0.1` refers to the local computer and can be used to access services running on that computer.

### Network Isolation

VirtualBox Internal Network allows VMs attached to the same internal network to communicate without directly connecting them to the physical LAN.

## 8. Troubleshooting Observations

- The initial APIPA address indicated that automatic address assignment was unavailable.
- Assigning a static IPv4 address resolved the addressing issue.
- Successful DNS resolution confirmed that the DC01 hostname could be translated into an IP address.
- DNS resolution alone does not establish that every Active Directory service is healthy.

## 9. Next Steps

- Verify LDAP SRV records.
- Test resolution of nonexistent DNS names.
- Add a Windows client VM to the same internal network.
- Perform client-to-server connectivity testing.
- Simulate and troubleshoot DNS configuration problems.

## 10. Outcome

DC01 has a verified static IPv4 configuration and successfully resolves its hostname using the lab DNS environment.
