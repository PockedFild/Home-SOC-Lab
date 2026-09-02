# Investigation 01: PowerShell Enumeration

## Scenario

A PowerShell command was intentionally executed on the `SOC-WIN11` endpoint
to test whether Sysmon and Wazuh could detect and record the activity.

The following command was executed:

`Get-LocalGroupMember -Group Administrators`

This command displays the members of the local Administrators group.

## Detection

Sysmon detected the PowerShell process and generated a Process Create event.

The event was collected by the Wazuh Agent and analyzed by the Wazuh Manager.
Wazuh generated an alert using rule `92027`.

Detection details:

- Endpoint: `SOC-WIN11`
- User: `SOC-WIN11\socuser`
- Provider: `Microsoft-Windows-Sysmon`
- Sysmon Event ID: `1`
- Wazuh Rule ID: `92027`
- Rule Level: `4`
- Description: `Powershell process spawned powershell instance`

## Investigation

The Sysmon event showed that `powershell.exe` was executed by the user
`SOC-WIN11\socuser`.

The recorded command line was:

`powershell.exe -NoProfile -Command "Get-LocalGroupMember -Group Administrators"`

The parent process was also `powershell.exe`, indicating that a PowerShell
process spawned another PowerShell instance.

Sysmon Event ID `1` provided useful process information including the user,
executable path, command line and parent process.

## Analysis

The executed command retrieves the members of the local Administrators group.

This command can be used legitimately by administrators to inspect local
group membership. However, similar commands may also be used during
reconnaissance to identify accounts with administrative privileges.

The Wazuh alert alone therefore does not prove malicious activity.
Additional context would normally be required to determine why the command
was executed.

In this lab, the command was intentionally executed as part of a controlled
detection test.

## Conclusion

The activity was classified as **Benign / Expected Test Activity**.

The test confirmed that Sysmon successfully recorded the PowerShell process
creation event and that Wazuh received and detected the activity.

This investigation demonstrated the basic SOC workflow of generating
activity, detecting it, examining the available telemetry and determining
whether the activity was malicious or benign.
