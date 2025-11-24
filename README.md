# Brute-Force-Attack-Detection-Incident-Response

# Overview

This project demonstrates my ability as a SOC Analyst to:
* Build a cloud-based detection environment
* Capture real-world brute force attacks
* Investigate alerts in Microsoft Sentinel
* Perform full Incident Response (IR) using industry-standard methodologies
* Apply security hardening controls after containment

This is a complete end-to-end SOC investigation—from attack → detection → investigation → response → prevention.

# 1. Lab Architecture: 
Cloud Setup
* Azure Windows 11 VM
* NSG configured initially to allow ALL inbound traffic (intentionally insecure)
* Windows Firewall turned OFF
* VM onboarded to:
* Microsoft Defender for Endpoint (MDE)
* Microsoft Sentinel via Log Analytics Workspace

Why?

To purposely expose the VM to the internet, collect real brute-force attack logs, and simulate a genuine SOC incident.

# 2. Attack Simulation (Real-World Brute Force Attempts)

After leaving the VM running for several hours, multiple external IPs began brute-forcing RDP.



Detected attacks came from four external IP addresses:



<img width="700" height="392" alt="Screen Shot 2025-11-24 at 4 42 20 pm" src="https://github.com/user-attachments/assets/018c674d-0c6a-4e62-9237-b16e8d94fa96" />

# 3. Detection Engineering

I created a Scheduled Analytics Rule in Microsoft Sentinel to detect brute-force attempts.

<img width="701" height="583" alt="Creating Analytics rule" src="https://github.com/user-attachments/assets/a6cb8591-b9f3-44fa-91a8-46a633fcd43d" />



<img width="700" height="347" alt="Analytics rule" src="https://github.com/user-attachments/assets/61c2a27d-7e02-4347-82bf-0dbcdbd7da7c" />

Outcome

Sentinel automatically triggered an Incident.
I assigned it to myself and changed status to Active.
Investigation started.

# 4. SOC Investigation
Verification of Successful Logins


<img width="701" height="172" alt="Shows logon success" src="https://github.com/user-attachments/assets/85e8d0a3-fc45-4513-a266-a754a8a48fc6" />

# Findings

* Brute-force attempts increased rapidly over time.
* Eventually, one of the attempts succeeded on win-ameer-proje.
* No lateral movement was detected (confirmed via MDE timeline & logs).


# 5. Incident Response (Containment → Eradication → Recovery)

Containment

* Isolated the compromised VM in Microsoft Defender for Endpoint.
* Blocked attacking IPs in NSG/firewall.
* Terminated active RDP sessions.

Eradication

* Ran a full Microsoft Defender Antivirus scan.
* Reviewed logs for signs of persistence:
* No suspicious tasks
* No new local users
* No unusual services or registry entries
* Hardened NSG rules (removed open RDP).

Recovery

* Reset passwords for all affected accounts.
* Restored the host to a clean state.
* Re-enabled the device after ensuring no active threats remained.

# 6. Post-Incident Security Improvements

To prevent future brute-force events:

Implemented

* Multi-Factor Authentication (MFA)
* Strong password & account lockout policies
* Updated Sentinel detection rules
* Restricted RDP to trusted IPs only

Recommended

* Azure Policy to prevent open NSGs
* Regular audits of exposed services & public ports


# 7. Final Incident Report

I documented the full event using a professional IR structure:

* Detection & Analysis
* Containment
* Eradication
* Recovery
* Post-Incident Improvements
* Closure

This demonstrated the full lifecycle of a SOC incident.

MITRE ATT&CK Mapping
Stage	              Technique                      	ID
Initial Access  	  Valid Accounts	              T1078
Initial Access	    Brute Force	                  T1110
Discovery	Remote    ystem Discovery	              T1018
Defense Evasion	    Disable Windows Firewall	    T1562.004


[Incident Report – Ameer Brute Force Scenario.pdf](https://github.com/user-attachments/files/23723019/Incident.Report.Ameer.Brute.Force.Scenario.pdf)


# 8. Conclusion

This project demonstrates my capabilities as a Security Operations Center (SOC) Analyst, including:

* Cloud security monitoring
* Log analysis
* KQL querying
* Incident investigation
* Microsoft Sentinel usage
* Incident response following best practices
* Security hardening and prevention
