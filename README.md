# Windows Endpoint Triage

## About This Project
In this project, I practiced basic Windows endpoint investigation using PowerShell and built-in Windows tools.
My goal was to understand how a SOC analyst can collect information from a Windows computer and use it to review users, processes, services, network connections, and login activity.

## What I Did
- Checked the computer and operating system information.
- Reviewed local user accounts and administrator access.
- Checked running processes and services.
- Matched network connections to process IDs.
- Reviewed Windows Security logs.
- Investigated successful and failed login events.
- Created a temporary test account to generate controlled login activity.
- Removed the test account after the investigation.

## Tools Used
- PowerShell
- Windows Security Logs
- `Get-WinEvent`
- `Get-Process`
- `Get-CimInstance`
- `netstat`
- `net user`
- `net localgroup`
- `auditpol`
