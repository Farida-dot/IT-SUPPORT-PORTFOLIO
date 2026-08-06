# Ticket 001 - Computer Unable to Browse Websites (APIPA Address)

## Incident Summary

A user reported that although the computer was connected to Wi-Fi, no websites could be accessed.


## Category

Network


## Priority

High


## Investigation

I verified the network configuration using `ipconfig`.

Findings:

- The computer had an APIPA address (169.254.x.x).
- No default gateway was assigned.

This indicated that the computer failed to obtain an IP address from the DHCP server.


## Troubleshooting Performed

- Checked the network configuration using `ipconfig`
- Attempted `ipconfig /release`
- Attempted `ipconfig /renew`

The issue persisted.


## Root Cause

The DHCP server did not assign an IP address to the client, so Windows automatically assigned an APIPA address.


## Next Steps

- Verify whether other users are affected.
- Check the DHCP server.
- Inspect the network connection.
- Escalate if the DHCP service is unavailable.

## Skills Demonstrated

- Windows Networking
- DHCP
- APIPA Troubleshooting
- Command Prompt
- Problem Solving
- Technical Documentation

## Lesson Learned

This exercise taught me how to identify DHCP failures using `ipconfig` and understand why Windows assigns an APIPA address when a DHCP server cannot be reached. 
