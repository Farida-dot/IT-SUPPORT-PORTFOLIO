# Active Directory Home Lab

## Overview
Hands-on Windows Server and Active Directory lab built with Microsoft Hyper-V to practice practical IT support and junior system administration skills.

> **Environment:** Personal/home lab — not production experience.

## Lab Architecture

| Component | Configuration |
|---|---|
| Hypervisor | Microsoft Hyper-V |
| Server | Windows Server 2025 Standard Evaluation |
| Server hostname | DC01 |
| Virtual switch | AD-Lab (Internal) |
| Hyper-V host adapter | 192.168.50.1/24 |
| DC01 | 192.168.50.10/24 |
| Active Directory domain | faridafixesIT.test |
| NetBIOS domain | FARIDAFIXESIT |
| DNS | DC01 / 192.168.50.10 |

```text
Physical Windows Host
        |
  192.168.50.1/24
        |
 vEthernet (AD-Lab)
        |
   Internal Switch
        |
  192.168.50.10/24
        |
       DC01
        |
 Active Directory
 faridafixesIT.test
```

## Phase 1 — Hyper-V and Windows Server

- Created a Generation 2 Windows Server VM.
- Configured the `AD-Lab` internal virtual switch.
- Renamed the server to `DC01`.
- Configured the host adapter as `192.168.50.1/24`.
- Configured DC01 with static `192.168.50.10/24`.
- Used `ipconfig`, `ping`, and `arp -a` for troubleshooting.
- Diagnosed an APIPA `169.254.x.x` address on DC01.
- Diagnosed ICMP blocking by Windows Firewall.
- Enabled the appropriate inbound ICMPv4 Echo Request rule.
- Verified final connectivity with 4/4 replies and 0% packet loss.

## Phase 2 — Active Directory Domain Services

Installed AD DS through Server Manager and promoted DC01 as the first domain controller in a new forest.

- Domain: `faridafixesIT.test`
- NetBIOS: `FARIDAFIXESIT`
- DNS: installed/configured
- Global Catalog: enabled
- AD DS prerequisites: passed

## Phase 3 — Organizational Units

Created:

```text
faridafixesIT.test
├── Finance
├── HR
├── IT
└── Sales
```

## Phase 4 — User Management

Created fictional test user **Sarah Mensah** in the Finance OU.

Used PowerShell to inspect the password policy:

```powershell
Get-ADDefaultDomainPasswordPolicy |
Select-Object MinPasswordLength,PasswordHistoryCount,ComplexityEnabled,ReversibleEncryptionEnabled
```

The lab reported a minimum length of 7 characters, complexity enabled, password history of 24, and reversible encryption disabled.

## Phase 5 — Account Lockout Policy

The initial lockout threshold was `0`, meaning lockout was disabled.

For this training lab I configured:

```powershell
Set-ADDefaultDomainPasswordPolicy `
  -Identity "faridafixesIT.test" `
  -LockoutThreshold 3 `
  -LockoutDuration "00:10:00" `
  -LockoutObservationWindow "00:10:00"
```

This supports a planned helpdesk exercise: identify a locked user account, unlock it, and verify authentication.

## Windows Time Troubleshooting

Post-promotion `dcdiag` reported a time-service/LocatorCheck warning. I investigated with:

```powershell
w32tm /query /status
w32tm /query /configuration
Get-Service w32time
w32tm /resync /rediscover
```

The Windows Time service was running and synchronization was tested. The VM also showed Hyper-V time synchronization as a source. This remains documented as a lab troubleshooting item rather than being presented as a production-ready configuration.

## Skills Demonstrated

- Hyper-V virtualization
- Windows Server administration
- Virtual switch configuration
- IPv4 addressing and subnetting
- APIPA troubleshooting
- ARP and ping troubleshooting
- Windows Firewall / ICMP troubleshooting
- Active Directory Domain Services
- Domain controller promotion
- DNS integration with AD
- Organizational Unit management
- User creation
- Password policy troubleshooting
- Account lockout policy configuration
- PowerShell administration
- Domain-controller diagnostics
- Windows Time troubleshooting
- Technical documentation

## Evidence

See the [`screenshots`](./screenshots/) folder for the lab evidence.

## Next Lab Tasks

- Complete the Sarah Mensah account-lockout exercise.
- Unlock and verify the account.
- Create additional users and security groups.
- Practice password resets and disabling/re-enabling accounts.
- Create a Windows client VM and join it to `faridafixesIT.test`.
- Create and test Group Policy Objects.
- Practice permissions and access-control scenarios.
- Document helpdesk-style tickets based on the lab.

## Disclaimer

This is a personal training environment using fictional users and data. It demonstrates hands-on learning and does not represent production administrative experience.
