# Findings & Evidence — Windows Forensics 1 (Registry)

This document shows **what artifact was used**, **where it lives**, and **what evidence supports the conclusion**.

---

## Evidence Index (Screenshots)
- `evidence_01_registryexplorer_ntuser_loaded.png` — Registry Explorer hive view
- `evidence_02_sam_user_accounts_table.png` — SAM users table (logons/users)
- `evidence_03_password_hint_thm-4n6.png` — THM-4n6 password hint
- `evidence_04_recentdocs_changelog_access.png` — RecentDocs entry for Changelog
- `evidence_05_userassist_python_installer_path.png` — UserAssist entry for python installer path
- `evidence_06_usb_last_connected.png` — USB device / last connected timestamp

---

## 1) User-created accounts present: **3**
**Artifact:** `SAM`  
**Registry location:** `SAM\Domains\Account\Users`  
**Method:** Use Registry Explorer “User accounts” view to distinguish default/built-in accounts vs user-created accounts.  
**Result:** 3 user-created accounts.  
**Evidence:** `evidence_02_sam_user_accounts_table.png`

---

## 2) Account that has never been logged in: **thm-user2**
**Artifact:** `SAM`  
**Registry location:** `SAM\Domains\Account\Users`  
**Method:** Review login count / last login time fields in Registry Explorer’s parsed account table.  
**Result:** `thm-user2` shows never logged in.  
**Evidence:** `evidence_02_sam_user_accounts_table.png`

---

## 3) Password hint for user THM-4n6: **count**
**Artifact:** `SAM`  
**Registry location:** `SAM\Domains\Account\Users`  
**Method:** Review password hint field in the parsed user table.  
**Result:** Password hint = `count`  
**Evidence:** `evidence_03_password_hint_thm-4n6.png`

---

## 4) `Changelog.txt` accessed time: **2021-11-24 18:18:48**
**Artifact:** RecentDocs (MRU)  
**Hive:** `NTUSER.DAT`  
**Registry location:** `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`  
**Method:** Use Registry Explorer “Recent documents” view and filter by extension where applicable (e.g., `.txt`).  
**Result:** `Changelog.txt` accessed at `2021-11-24 18:18:48`  
**Evidence:** `evidence_04_recentdocs_changelog_access.png`

---

## 5) Python 3.8.2 installer executed from: **Z:\setups\python-3.8.2.exe**
**Artifact:** UserAssist (Explorer-launched programs)  
**Hive:** `NTUSER.DAT`  
**Registry location:** `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count`  
**Method:** Use Registry Explorer “UserAssist” view to identify executed program name/path.  
**Result:** Execution evidence shows installer path `Z:\setups\python-3.8.2.exe`  
**Evidence:** `evidence_05_userassist_python_installer_path.png`

> Interpretation: `Z:` typically indicates a mapped/network drive in many environments. This supports the scenario claim that the system connected to a network drive/share.

---

## 6) USB device (friendly name “USB”) last connected: **2021-11-24 18:40:06**
**Artifact:** USB device enumeration / connection timestamps  
**Hive:** `SYSTEM` (and sometimes correlated with SOFTWARE portable device entries)  
**Registry location examples:**
- `SYSTEM\CurrentControlSet\Enum\USBSTOR`
- `SYSTEM\CurrentControlSet\Enum\USB`
**Method:** Use Registry Explorer parsed USBSTOR view to identify device + timestamps.  
**Result:** Last connected time = `2021-11-24 18:40:06`  
**Evidence:** `evidence/06_usb_last_connected.png`
