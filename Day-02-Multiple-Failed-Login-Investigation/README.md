# Week 12 – Day 2: Multiple Failed Login Investigation

## Objective
Investigate repeated Windows failed-login events using Wazuh and examine their timestamps, source addresses, and authentication details.

## Environment
- SIEM: Wazuh
- Endpoint: Windows Server 2022
- Agent: WinServ22
- Agent ID: 003

## Findings

I searched Wazuh for Windows Event ID 4625 associated with the Administrator account over a 90-day period. I found 17 matching events.

I examined several records and identified three failed-login events on October 29, 2026, occurring within approximately 11 seconds.

The events showed:
- Source IP: 127.0.0.1
- Logon type: 2 (Interactive)
- Status: 0xc000006d
- Substatus: 0xc000006a
- Workstation: WINSERV22

I also identified a successful Administrator login (Event ID 4624) on October 29 at 14:29:40.724. Its logon type was 7 (Unlock), and the workstation was WINSERV22.

The successful login occurred before the three failed attempts. Therefore, the records do not establish a successful login following that cluster of failures.

## Conclusion

Wazuh collected multiple failed Administrator login events. Three events occurred within a short period and reported an incorrect password. The source address was the local loopback address, 127.0.0.1.

The available evidence identifies repeated failed local interactive login attempts, but it does not establish malicious activity or a brute-force attack.

## Skills Practiced
- Searching Windows authentication events in Wazuh
- Comparing Event IDs 4624 and 4625
- Interpreting Windows logon types
- Reviewing authentication status and substatus codes
- Examining timestamps and identifying event patterns
- Distinguishing local loopback addresses from remote IP addresses
