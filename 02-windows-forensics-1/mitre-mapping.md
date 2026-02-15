# MITRE ATT&CK Mapping (Based on Observed Artifacts)

This mapping does not claim an intrusion occurred; it maps **what these artifacts are commonly used to validate** during investigations.

## Techniques
- **T1078 – Valid Accounts**
  - Relevance: Multiple accounts and account usage validation in SAM supports investigations of unauthorized access via accounts.

- **T1083 – File and Directory Discovery**
  - Relevance: RecentDocs/MRU artifacts can show file interaction patterns consistent with user navigation and discovery.

- **T1059 – Command and Scripting Interpreter (contextual)**
  - Relevance: Installer execution can be paired with later scripting; UserAssist documents GUI-launched executables (not cmd-only).

- **T1021.002 – Remote Services: SMB/Windows Admin Shares (contextual)**
  - Relevance: Execution path from `Z:` suggests a mapped share / network drive which is commonly SMB-backed in enterprise environments.

- **T1092 / T1105 (contextual, data movement hypotheses)**
  - Relevance: USB connection timing can be used when investigating potential staged data transfer.

## Defensive / Investigation Notes
Registry artifacts are often used to:
- Confirm program execution (UserAssist, AmCache, ShimCache, BAM/DAM)
- Confirm persistence locations (Run/RunOnce, Services)
- Confirm removable media usage (USBSTOR/USB)
- Corroborate timelines (LastWrite timestamps, MRU ordering)
