# Windows Forensics 1 (TryHackMe) — Windows Registry Artifacts Case Study

## Overview
This project demonstrates Windows host-based forensic analysis using **Windows Registry artifacts**. It includes both:
1) **Foundational registry artifact knowledge** (hives, locations, tools), and  
2) A **hands-on investigation** (THM challenge) using triage data and Eric Zimmerman tools to answer questions for a suspected unauthorized access scenario.

## Scenario (Challenge)
Organization X suspects a research lab desktop was accessed by an unauthorized person. Analysts observed:
- Multiple user accounts (unusual for a single-user workstation)
- A network drive mapping
- A USB device connection

Triage data was collected (KAPE-style structure) and analyzed offline.

## Tools Used
- **Eric Zimmerman Registry Explorer** (dirty hive + transaction log merge, bookmarks)
- **EZViewer** (reviewing parsed output when applicable)
- Windows triage registry hives: `SAM`, `SYSTEM`, `SOFTWARE`, `NTUSER.DAT`, `USRCLASS.DAT`, plus transaction logs

## Skills Demonstrated
- Registry hive identification and offline analysis workflow  
- User account enumeration and account usage validation (SAM)  
- Recent file activity via MRU/RecentDocs keys  
- Program execution evidence via UserAssist  
- USB connection evidence via SYSTEM enumeration/USBSTOR  
- Investigation documentation + evidence handling (screenshots + report style)

## Key Findings (Challenge Answers)
- **User-created accounts:** 3  
- **Account never logged in:** `thm-user2`  
- **Password hint (THM-4n6):** `count`  
- **File accessed:** `Changelog.txt` at `2021-11-24 18:18:48`  
- **Python installer execution path:** `Z:\setups\python-3.8.2.exe`  
- **USB last connected (friendly name “USB”):** `2021-11-24 18:40:06`

> Full evidence and registry locations are documented in `findings.md` with screenshot references.

## Repository Contents
- `incident-summary.md` — 1-page IR-style summary
- `findings.md` — evidence, registry paths, and how each conclusion was reached
- `mitre-mapping.md` — ATT&CK technique mapping based on observed artifacts
- `containment-eradication.md` — what to do if this were a real incident
- `business-impact.md` — leadership-focused impact paragraph (MBA layer)
- `evidence/` — supporting screenshots (sanitized)

## Notes / Ethics
This repo focuses on **forensic methodology** and **artifact interpretation**. No exploitation steps, malware development, or misuse instructions are included.
