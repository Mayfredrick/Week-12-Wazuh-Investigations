#  Day 6: Windows Group Membership Removal Investigation

## Objective
Investigate Windows security events associated with removing members from security-enabled groups.

## Lab Environment
- SIEM: Wazuh
- Endpoint: Windows Server 2022
- Agent: WinServ22
- Time range: Last 90 days

## Investigation

### Event ID 4729
- Description: A member was removed from a security-enabled global group.
- Wazuh search returned no matching events.

### Event ID 4733
- Description: A member was removed from a security-enabled local group.
- Wazuh search returned no matching events.

## Findings
No matching group membership removal events were found in the available Wazuh data for the selected 90-day period.

The absence of matching records does not prove that no group membership removals occurred. Events may not have been generated, collected, or retained.

## Conclusion
Completed an investigation of Windows group membership removal events using Wazuh. Reviewed Event IDs 4729 and 4733 and documented the search results.

## Skills Practiced
- Windows security event monitoring
- Active Directory group management concepts
- Wazuh Threat Hunting
- Event ID investigation
- Security event documentation
