# Active-Directory-Enumeration-with-Nmap
# Active Directory Enumeration with Nmap

## Overview

This project documents the initial reconnaissance phase against my Windows Server 2019 Active Directory Domain Controller within my cybersecurity homelab.

The objective was to identify:

- Open ports
- Running services
- Active Directory components
- Operating system information
- Remote management services

---

## Lab Environment

| System | Details |
|----------|----------|
| Attacker Machine | Kali Linux |
| Target Machine | Windows Server 2019 |
| Role | Active Directory Domain Controller |
| Domain | MyLab.local |
| Target IP | 192.168.56.10 |
| Network Type | VMware Host-Only Network |

---

## Nmap Scan

### Command

```bash
nmap -sV -O 192.168.56.10
```

### Purpose

- Service Version Detection (`-sV`)
- Operating System Detection (`-O`)

---

## Scan Results

```text
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  ncacn_http
636/tcp  open  tcpwrapped
3268/tcp open  ldap
3269/tcp open  tcpwrapped
3389/tcp open  ms-wbt-server
5985/tcp open  http
```

---

## Service Breakdown

### DNS (53)

Active Directory relies on DNS for locating domain resources and authentication services.

### Kerberos (88)

Primary authentication protocol used by Active Directory.

### RPC (135)

Microsoft Remote Procedure Call service used for Windows administration and communication between services.

### NetBIOS (139)

Legacy Windows networking protocol commonly used alongside SMB.

### LDAP (389)

Directory service responsible for storing and providing information about:

- Users
- Computers
- Groups
- Organizational Units

Discovered Domain:

```text
MyLab.local
```

### SMB (445)

Provides access to:

- Shared folders
- SYSVOL
- NETLOGON
- Administrative shares

### Kerberos Password Service (464)

Enables password changes using Kerberos.

### RPC over HTTP (593)

Supports remote management and administration traffic.

### LDAPS (636)

Encrypted LDAP communications over SSL/TLS.

### Global Catalog (3268)

Provides forest-wide directory search capabilities.

### Secure Global Catalog (3269)

Encrypted version of the Global Catalog service.

### RDP (3389)

Microsoft Remote Desktop Services available for remote administration.

### WinRM (5985)

Windows Remote Management service used by:

- PowerShell Remoting
- Automation tools
- Remote administration

---

## Operating System Detection

Nmap identified the target as:

```text
Microsoft Windows 2019/10/11 (97% confidence)
```

Based on the lab configuration, this host is a:

```text
Windows Server 2019 Active Directory Domain Controller
```

---

## Key Findings

✅ Active Directory Domain Controller Detected

✅ Domain Name Identified

✅ DNS Service Running

✅ LDAP Service Running

✅ Kerberos Authentication Running

✅ SMB File Sharing Available

✅ RDP Enabled

✅ WinRM Enabled

✅ Global Catalog Available

---

## Skills Demonstrated

- Network Reconnaissance
- Nmap Enumeration
- Service Identification
- Active Directory Discovery
- Attack Surface Mapping
- Documentation & Reporting

---

## Lessons Learned

A single Nmap scan can reveal valuable information about an Active Directory environment without authentication. Enumerating open ports and services helps identify:

- Authentication mechanisms
- Directory services
- File sharing protocols
- Remote management interfaces
- Potential attack paths

Understanding these services is an essential step in both blue team monitoring and red team reconnaissance.

---

## Next Steps

Conduct deeper enumeration using:

```bash
nmap -sC -sV 192.168.56.10
```

Future projects will include:

- SMB enumeration
- LDAP enumeration
- BloodHound data collection
- Group Policy analysis
- Windows event log monitoring with Splunk
- Security monitoring with Wazuh
