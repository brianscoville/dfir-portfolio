# Incident Summary — Windows Registry Artifacts Investigation (THM Windows Forensics 1)

## Executive Summary
A suspected unauthorized access incident was investigated on a Windows workstation using offline triage data. Registry artifacts were analyzed to validate:
- Presence of multiple user accounts (unusual for the environment)
- Recently accessed files
- Evidence of program execution
- Evidence of USB device connectivity

Registry analysis confirmed **3 user-created accounts**, identified an account with **no successful logons**, confirmed access to `Changelog.txt`, showed execution of a **Python 3.8.2 installer from a mapped/network drive (Z:)**, and validated the last connection time of a USB device with friendly name “USB”.

## Scope
- Evidence source: triage data (registry hives + transaction logs)
- Primary artifacts: `SAM`, `SYSTEM`, `SOFTWARE`, `NTUSER.DAT`, `USRCLASS.DAT`
- Tools: Eric Zimmerman Registry Explorer

## Key Findings
- **User created accounts:** 3  
- **Account never logged in:** `thm-user2`  
- **Password hint for THM-4n6:** `count`  
- **Recent file access:** `Changelog.txt` accessed at `2021-11-24 18:18:48`  
- **Execution evidence:** Python installer run from `Z:\setups\python-3.8.2.exe`  
- **Removable media:** USB device last connected at `2021-11-24 18:40:06`

## Analyst Assessment (What this suggests)
- Multiple accounts and a never-used account can indicate shared usage, misconfiguration, or preparation for unauthorized access.
- Execution from `Z:` strongly suggests interaction with a mapped drive / network share (common in lab environments).
- RecentDocs + UserAssist provide user-activity indicators; USB connection timing may be relevant for data movement hypotheses.

## Recommendations (High-level)
- Validate account legitimacy and ownership; disable or remove unnecessary accounts.
- Audit mapped drives and restrict execution from network shares.
- Enhance logging/monitoring for registry persistence keys and removable media events.
- Preserve full disk + memory acquisition if active compromise suspected.
