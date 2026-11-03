# Week 12 – Day 3: Windows Account Activity Investigation

## Objective
Investigate Windows account-management events using Wazuh and identify account-enablement activity.

## Environment
- SIEM: Wazuh
- Endpoint: Windows Server 2022
- Agent: WinServ22
- Agent ID: 003
- Domain: HOMELAB

## Investigation

I searched Wazuh for Windows Event ID 4720 over the last 90 days. No matching account-creation events were found.

I then searched for Event ID 4722, which represents a user account being enabled. Wazuh returned four matching events.

## Findings

All four events occurred on October 22, 2026.

| Target account | Timestamp | Subject account |
|---|---|---|
| WIN10$ | 21:54:22.670 | Administrator |
| ITPC01$ | 21:54:45.898 | Administrator |
| ITPC02$ | 21:54:53.783 | Administrator |
| ADIT10$ | 21:55:12.928 | Administrator |

All four target accounts belonged to the HOMELAB domain. Each event identified Administrator as the account performing the action.

The four events occurred within approximately 50 seconds.

## Conclusion

Wazuh collected four account-enablement events involving different computer accounts. The events were recorded under the Administrator account.

The investigation demonstrated how to use Windows Event IDs 4720 and 4722 to distinguish account creation from account enablement.

The available records do not establish why these accounts were enabled or whether the activity was authorized.

## Skills Practiced
- Searching account-management events in Wazuh
- Understanding Windows Event ID 4720
- Understanding Windows Event ID 4722
- Identifying target and subject accounts
- Comparing timestamps across security events
- Documenting findings without assuming malicious activity
