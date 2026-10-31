# Day 1: Correlating Windows Authentication Events with Network Configuration

## Lab Environment

- SIEM: Wazuh
- Endpoint: Windows Server 2022
- Agent: WinServ22
- Agent ID: 003
- Wazuh Manager: 192.168.114.19
- VMware Network: VMnet8

## Objective

Investigate Windows authentication events and compare the source IP information in Wazuh with the network configuration of the monitored Windows Server.

## 1. Failed Login Investigation

Searched for Windows Event ID 4625 over the last 24 hours.

**Result:** No matching events were found.

## 2. Successful Login Investigation

Located a Windows Event ID 4624 alert.

Findings:

| Field | Value |
|---|---|
| Username | WINSERV22$ |
| Domain | HOMELAB.LOCAL |
| Logon Type | 3 |
| Source IP | fe80::40f1:949f:6ba1:2059 |
| IP Port | 56258 |
| Workstation | WinServ22.homelab.local |
| Authentication Package | Kerberos |
| Logon Process | Kerberos |

Event ID 4624 indicates a successful logon. Logon type 3 indicates a network logon.

## 3. IPv6 Address Verification

Used PowerShell on Windows Server 2022 to inspect the network interfaces.

Commands used:

```powershell
Get-NetIPAddress -AddressFamily IPv6 |
Format-Table InterfaceAlias, IPAddress, AddressState
```

```powershell
Get-NetIPConfiguration -InterfaceAlias "Ethernet0"
```

```powershell
Get-NetIPAddress -InterfaceAlias "Ethernet0" |
Format-Table AddressFamily, IPAddress, PrefixLength, AddressState
```

```powershell
Get-NetAdapter -Name "Ethernet0" |
Format-List Name, Status, MacAddress, LinkSpeed
```

## 4. Network Verification Results

| Item | Value |
|---|---|
| Interface | Ethernet0 |
| IPv4 | 192.168.114.12 |
| IPv6 | fe80::40f1:949f:6ba1:2059 |
| Interface Status | Up |
| MAC Address | 00-0C-29-9E-48-A5 |
| VMware Network | VMnet8 |

The IPv6 address in the Wazuh alert matched the IPv6 address assigned to Ethernet0.

The IPv4 address matched the Wazuh agent's recorded IP address.

## 5. Investigation Conclusion

The investigation identified a successful network logon using Kerberos authentication. The source IPv6 address was verified against the Windows Server network configuration.

No matching failed-login event was found in the selected 24-hour search period. Therefore, this investigation did not establish a failed-login-then-successful-login sequence.

The activity was consistent with network authentication involving the monitored Windows Server. No evidence from the reviewed fields established malicious activity.

## Lessons Learned

- How to investigate Windows Event IDs 4624 and 4625 in Wazuh.
- How to interpret Windows logon type 3.
- How Kerberos authentication is represented in Windows Security events.
- How to identify IPv4 and IPv6 addresses.
- How to use PowerShell to inspect Windows network interfaces.
- How to compare SIEM event data with endpoint network configuration.

This exercise helped me understand the importance of validating alert information against the monitored endpoint before drawing security conclusions.
