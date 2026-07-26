# Suspicious Windows Logon Investigation

**Source:** Coursework-derived scenario, independently rewritten  
**Status:** Complete case study  
**Severity:** Medium  
**Times:** Relative UTC

## Executive summary

Multiple failed logons for a fictional administrator account were followed by a success from the same workstation. The sequence required investigation because it could represent password guessing, a stale saved credential, or an administrator mistyping a password.

Correlation showed that the source was a managed help-desk workstation, the successful logon used the expected interactive type, and no privileged changes followed. The account owner confirmed the activity. The case was closed as benign user error with a recommendation to monitor recurrence.

## Evidence inventory

| Evidence | Purpose |
|---|---|
| Security events `4625` and `4624` | Failed and successful logon sequence |
| Event `4740`, if present | Account-lockout context |
| Endpoint inventory | Source ownership and management status |
| Authentication-policy data | Lockout threshold and audit coverage |
| Account-owner confirmation | Authorization context, not sole technical proof |

## Timeline

| Relative time | Event | Interpretation |
|---|---|---|
| T0 | First failed interactive logon | Could be a typo or initial guessing attempt |
| T+35 sec | Four additional failures from the same host | Pattern requires correlation |
| T+62 sec | Successful logon from the same host | Credential was eventually accepted |
| T+4 min | Normal help-desk tools opened | No evidence of unusual execution |
| T+18 min | Owner confirms password-entry errors | Supports benign disposition |

## Analysis

Event volume alone is insufficient. The analyst reviews the target account, source host, logon type, authentication package, failure reason, session activity, and whether the source has attempted other accounts. A single source trying many users would raise concern for password spraying; many sources targeting one user would suggest a different pattern.

## Disposition

**Benign positive — moderate confidence.** The sequence is consistent with user error and the source is expected. Confidence is not high because the case uses a limited synthetic evidence set.

## Recommendations

- Alert on repeated failures followed by success for privileged identities.
- Distinguish one-user guessing from one-password-many-users spraying.
- Enrich alerts with asset ownership and account privilege.
- Review saved credentials if the pattern recurs.
- Preserve the original event fields before summarizing them.
