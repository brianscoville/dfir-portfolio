# Containment, Eradication, and Recovery (If this were a real incident)

## Containment (Immediate)
- Isolate host from network (preserve state)
- Preserve evidence:
  - Full disk image if feasible
  - Memory acquisition (if suspected active compromise)
  - Secure triage artifacts (hives + logs)
- Disable/lock suspicious or unneeded accounts pending validation

## Eradication
- Remove unauthorized accounts; enforce least privilege
- Reset credentials for affected users; rotate local admin passwords
- Restrict execution from network shares (e.g., AppLocker/WDAC policies)
- Review persistence locations:
  - Run/RunOnce keys (HKCU/HKLM)
  - Services in `SYSTEM\CurrentControlSet\Services`
  - Scheduled tasks and startup folders (not registry-only)

## Recovery
- Rejoin to domain / reimage if compromise confirmed
- Re-enable access gradually with monitoring
- Validate mapped drive policies and share permissions

## Hardening / Prevention
- Enable enhanced auditing for logons + removable media
- Deploy EDR rules for suspicious registry modifications
- Monitor for unusual creation of local accounts on lab systems
