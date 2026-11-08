# Week 12 – Day 07 Windows Authentication and Active Directory Security Monitoring

## Objective
Investigate Windows authentication events, account management activities, and Active Directory group membership changes using Wazuh.

## Lab Environment
- SIEM: Wazuh
- Endpoint: Windows Server 2022
- Agent: WinServ22
- Directory Services: Active Directory
- Investigation period: 90 days for historical searches

## Activities Performed

### Day 1 – Authentication Event Correlation
- Investigated Event ID 4624 (successful logon).
- Investigated Event ID 4625 (failed logon).
- Reviewed logon type, workstation, and source address.
- Confirmed that the observed IPv6 source address belonged to the endpoint itself.

### Day 2 – Failed Login Investigation
- Reviewed repeated failed login events.
- Identified three failed Administrator logons within approximately 11 seconds.
- Reviewed status and substatus codes.
- Confirmed that the events used the local loopback address 127.0.0.1.
- Did not classify the activity as malicious without further evidence.

### Day 3 – Account Activity
- Investigated Event IDs 4720 and 4722.
- Found four account enablement events.
- Identified the accounts WIN10$, ITPC01$, ITPC02$, and ADIT10$.
- Confirmed that Event ID 4722 represents account enablement, not account creation.

### Day 4 – Account Modification
- Investigated Event IDs 4725, 4726, and 4738.
- Found an account modification event involving john.admin.
- Reviewed the anonymous logon subject and process ID.
- Could not establish which process caused the modification or what specific attribute changed.

### Day 5 – Group Membership Additions
- Investigated Event IDs 4732 and 4728.
- Found two Event ID 4728 records.
- Identified John Admin being added to Sales1.
- Identified Sales1 being added to Domain Admins.
- Used PowerShell to verify that Sales1 is a global security group and that john.admin is a member.
- Verified the nested group membership relationship.

### Day 6 – Group Membership Removals
- Investigated Event IDs 4729 and 4733.
- No matching events were found in the available Wazuh data for the selected 90-day period.

### Day 7 – Security Assessment
Reviewed the risks associated with nested group membership and elevated privileges.

Key observations:
- Adding a group to Domain Admins can grant its members elevated privileges.
- Group membership changes should be reviewed for authorization and business need.
- A recorded event does not automatically establish malicious activity.
- Additional investigation is necessary to determine whether an event represents legitimate administration or suspicious activity.

## Key Findings
The investigation identified account activity and group membership changes in the Windows Server 2022 environment.

The nested relationship between john.admin, Sales1, and Domain Admins demonstrated how group membership can affect privilege levels.

No matching records for certain event searches does not establish that the activities never occurred. Findings are limited to the available Wazuh data and selected search periods.

## Skills Practiced
- Wazuh Threat Hunting
- Windows Security Event Analysis
- Active Directory Administration
- PowerShell Group Membership Verification
- Authentication Monitoring
- Privilege and Access Review
- Security Investigation Documentation

## Conclusion
Completed a seven-day investigation focused on Windows authentication, account management, and Active Directory group membership monitoring. Practiced identifying security-relevant events, validating findings with PowerShell, and documenting investigation limitations without assuming malicious activity.
