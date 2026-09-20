# Active Directory Lab — Troubleshooting Notes

## 1. DC01 received an APIPA address

**Symptom:** DC01 showed a `169.254.x.x` address.

**Investigation:**
```powershell
ipconfig /all
```

**Cause:** The isolated Hyper-V internal network did not provide DHCP.

**Resolution:** Configured DC01 with static `192.168.50.10/24`.

---

## 2. Host could not initially ping DC01

**Symptom:** Ping returned timeouts.

**Investigation:**
```text
ping 192.168.50.10
arp -a
```

ARP was then used to verify Layer 2 discovery.

**Resolution:** After confirming the virtual network and static addresses, the appropriate inbound ICMPv4 Echo Request firewall rule was enabled.

**Verification:**
```text
Sent = 4
Received = 4
Lost = 0 (0% loss)
```

---

## 3. New AD user password was rejected

**Investigation:**
```powershell
Get-ADDefaultDomainPasswordPolicy |
Select-Object MinPasswordLength,PasswordHistoryCount,ComplexityEnabled,ReversibleEncryptionEnabled
```

**Finding:** Minimum length 7; complexity enabled; history 24; reversible encryption disabled.

**Resolution:** Created Sarah Mensah with a compliant lab password.

---

## 4. Account lockout was disabled

**Finding:**
```text
LockoutThreshold: 0
```

A threshold of zero disables account lockout.

**Training-lab configuration:**
```powershell
Set-ADDefaultDomainPasswordPolicy `
  -Identity "faridafixesIT.test" `
  -LockoutThreshold 3 `
  -LockoutDuration "00:10:00" `
  -LockoutObservationWindow "00:10:00"
```

---

## 5. Domain-controller time diagnostics

`dcdiag` reported a time-service/LocatorCheck warning. I checked:

```powershell
w32tm /query /status
w32tm /query /configuration
Get-Service w32time
```

The Windows Time service was running, synchronization was attempted, and Hyper-V VM time synchronization was visible as a source. This remains a documented lab troubleshooting item for further investigation.

## Troubleshooting Method

1. Identify the symptom.
2. Gather evidence.
3. Check configuration.
4. Form a likely cause.
5. Make the smallest appropriate change.
6. Test again.
7. Document the result.
