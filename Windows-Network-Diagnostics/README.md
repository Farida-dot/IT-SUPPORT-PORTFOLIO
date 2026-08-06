# Windows Network Diagnostics Lab

## Objective

The objective of this lab was to learn how to use Windows networking tools to diagnose and troubleshoot connectivity issues in Windows.

## Environment

- Operating System: Windows 11 Pro
- Connection Type: Home Wi-Fi
- Tools Used:
- Command Prompt
- ipconfig
- ipconfig /all
- ping
- tracert
- nslookup

---

## Scenario

This lab was performed to understand how Windows networking commands can be used to verify network connectivity, identify IP configuration issues, test DNS resolution, and troubleshoot common network problems.

---

## Commands Used

### ipconfig /all

Purpose:
Displays detailed network information including DHCP server, DNS SERVERS, MAC Address, and lease information.

**Screenshot**
{ipconfig /all} {screenshots/ipconfig.png}

Observation:
The computer is successfully connected to a DHCP server, has a MAC address and a lease information.


---

### ipconfig 

Purpose:
Displays the computer's IP address, subnet mask, and default gateway.

**Screenshot**
{ipconfig} {screenshot/ipconfig.png}

Observation:
The computer received a valid IPv4 address from the DHCP server. The subnet mask and default gateway were also assigned correctly, indicating the network configuration was succesful.

---

### ping

Purpose:
Tests connectivity between the computer and another device or website.

**Screenshots**
{ping} {screenshot/ping.png}

Observation:
Google was responsive and there 0 packet loss , showing connectivity was working.

---

### tracert

Purpose:
Shows the path packets take across the network.

**Screeenshots**
{tracert} [Screenshot/tracert.png}
Observation:
some hops timed out because a few routers do not respond to traceroute requests, but trace still reached successfully

---

### nslookup

Purpose:
Checks whether DNS can resolve domain names into IP addresses.

**Screenshot**
{nslooup} {screenshot/nslookup.png}

Observation:
DNS successfully resolvedgoogle.com to multiple IP4 and IPV6 addresses 

---

## Skills Demonstrated

- Windows Networking
- Network Troubleshooting
- DNS
- DHCP
- Command Prompt
- Technical Documentation

---

## Lessons Learned

This lab improved my understanding of how Windows networking commands help identify and troubleshoot connectivity issues.
