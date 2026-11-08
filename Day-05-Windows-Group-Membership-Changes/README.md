# Day 5: Windows Group Membership Investigation

## Objective
Investigate Windows security group membership changes using Wazuh and verify the current Active Directory group relationships.

## Events Investigated

### Event ID 4732 – Member Added to Security-Enabled Local Group
- Searched the last 90 days.
- No matching events were found in the available Wazuh data.

### Event ID 4728 – Member Added to Security-Enabled Global Group
Two matching events were identified on October 23, 2026.

**Event 1**
- Target group: Domain Admins
- Added member: Sales1
- Initiating account: Administrator

**Event 2**
- Target group: Sales1
- Added member: John Admin
- Initiating account: Administrator

The two events occurred approximately 43 milliseconds apart.

## Active Directory Verification

PowerShell confirmed that:
- Sales1 is a global security group.
- John Admin (`john.admin`) is currently a member of Sales1.
- Sales1 is currently a member of Domain Admins.

The group membership chain is:
Domain Admins
└── Sales1
    └── John Admin

## Security Observation

The nested group membership means John Admin can receive Domain Admin privileges through membership in Sales1.

This is a significant privilege assignment that should be reviewed and authorized. The available events do not establish whether the changes were approved or whether the privileges were used.

## Conclusion

This investigation identified two group membership changes and verified that the nested memberships currently exist in Active Directory. No matching Event ID 4732 records were found in the selected 90-day search.

The exercise demonstrated how Wazuh event records can be correlated with PowerShell Active Directory queries to investigate group membership and potential privilege exposure.
