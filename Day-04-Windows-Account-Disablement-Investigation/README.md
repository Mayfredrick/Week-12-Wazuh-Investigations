# Day 4: Windows Account Disablement and Modification Investigation

## Objective
Investigate Windows account disablement, deletion, and modification events using Wazuh.

## Environment
- SIEM: Wazuh
- Endpoint: Windows Server 2022
- Agent: WinServ22
- Agent ID: 003
- Domain: HOMELAB

## Investigation Results

| Event ID | Activity | Result |
|---|---|---|
| 4725 | Account disabled | No matching events |
| 4726 | Account deleted | No matching events |
| 4738 | Account modified | Matching event found |

## Account Modification Finding

Wazuh identified an Event ID 4738 on October 23, 2026, at 04:03:12.348.

Observed details:
- Target account: john.admin
- Target domain: HOMELAB
- Subject account: ANONYMOUS LOGON
- Subject SID: S-1-5-7
- Subject Logon ID: 0x3e6
- Process ID: 696

## Process Investigation

I checked Windows Security logs for Event ID 4688 to identify the process associated with PID 696.

No matching process-creation event was found for October 23 around the account-modification timestamp.

The process responsible for the event could not be identified from the available logs.

## Conclusion

Wazuh recorded an account-modification event involving john.admin. The event identified ANONYMOUS LOGON as the subject.

The investigation did not establish what account attribute was changed, why the event occurred, or which process was responsible.

No matching account-disablement or account-deletion events were found in the selected 90-day period.

## Skills Practiced
- Searching Windows Security events in Wazuh
- Understanding Event IDs 4725, 4726, and 4738
- Examining Windows account-management records
- Reviewing security identifiers and logon IDs
- Investigating process IDs
- Comparing Wazuh alerts with Windows Event Viewer
- Documenting findings and investigation limitations
