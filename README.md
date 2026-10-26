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

## System Information
I started by checking the basic information about the computer I was investigating. This helped me confirm the operating system architecture, manufacturer, and device model before moving into the rest of the investigation.

![System Information](screenshots/System%20information.png)

## Local Administrators

I checked the local Administrators group to see which accounts had elevated access on the computer. This helped me understand who had administrative privileges before moving further into the investigation.

![Local Administrators](screenshots/Local%20Adminstrators.png)

## Running Processes

I reviewed the running processes and their process IDs (PIDs). This helped me see which programs were active on the computer and gave me a starting point for checking anything unusual.

![Running Processes](screenshots/Running%20Process.png)

## Network Connections

I used `netstat` to check active network connections and the PIDs linked to them. I compared some of the PIDs with the running processes to understand which applications were making network connections.

![Network Connections](screenshots/Network%20Connection.png)

## Authentication Log Investigation

I reviewed Windows Security logs to understand successful and failed login activity.

I learned that an Event ID alone does not tell the full story. The account name, logon type, source address, and failure reason provide more information about what happened.

### Failed Login - Event ID 4625

I created a temporary account called `soclab` and generated a controlled failed network login using an incorrect password.

The event showed:

- Event ID: `4625`
- Account: `soclab`
- Logon Type: `3`
- Source Address: `127.0.0.1`
- Failure Reason: Incorrect password

![Failed Logon](screenshots/Failed%20Logon.png)

### Successful Login - Event ID 4624

I repeated the network login using the correct password and confirmed that Windows recorded a successful login for the same account.

The event showed:

- Event ID: `4624`
- Account: `soclab`
- Logon Type: `3`

![Successful Logon](screenshots/Sucessful%20logon.png)

## Key Findings

- I confirmed the basic system information and administrator accounts on the endpoint.
- I reviewed running processes and active network connections.
- I generated a controlled failed login and found the related Event ID `4625`.
- I repeated the login with the correct password and found Event ID `4624`.
- I did not find anything from this exercise that showed the system was compromised.

## Troubleshooting

At first, I could not access the Windows Security log because PowerShell was not running with administrator privileges. I reopened PowerShell as Administrator and was able to access the logs.

I also tried using `runas` to generate a failed login, but it did not create the event I needed. I changed my approach and used a network authentication attempt instead.

## What I Learned

This project helped me understand how different pieces of Windows information can be connected during an investigation.

I learned how to:

- Check local users and administrator privileges.
- Review running processes.
- Match network connections to PIDs.
- Review Windows Security logs.
- Recognize Event IDs `4624` and `4625`.
- Understand different logon types.
- Compare successful and failed login activity.
- Avoid making conclusions without enough evidence.

## Conclusion

This project gave me practical experience with basic Windows endpoint triage.

Instead of only reading about Windows logs and authentication events, I generated controlled login activity, found the events myself, and reviewed the evidence to understand what happened.
