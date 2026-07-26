# Phishing Investigation

**Source:** Independent simulated case  
**Status:** Complete case study  
**Severity:** High until credential exposure is ruled out

## Executive summary

A fictional employee reports an unexpected document-sharing message that pressures the recipient to sign in through an external link. The display name imitates a trusted service, but the sender domain and authentication results do not support the claimed identity.

The simulated user did not submit credentials. The message is classified as credential phishing, removed from other mailboxes in the scenario, and used to create detection and awareness improvements.

## Evidence inventory

- original message preserved as a safe text representation;
- full mail headers;
- sender, reply-to, return path, and authentication results;
- normalized URL and redirect chain reviewed in a safe environment;
- message trace for other recipients; and
- sign-in records for the targeted identity.

## Findings

| Observation | Interpretation |
|---|---|
| Display name imitates a file-sharing service | Social-engineering indicator |
| Sender domain differs from the claimed service | Strong identity mismatch |
| Reply-to points to another domain | Attempt to redirect responses |
| Authentication results fail or do not align | Sender is not authorized as claimed |
| URL uses an unrelated host and a login-themed path | Consistent with credential collection |
| No matching user sign-in after delivery | No observed credential use in the review window |

## Response

1. Quarantine or remove matching messages.
2. Block the confirmed malicious indicators with an expiration and owner.
3. Search for recipients, clicks, replies, and forwarded copies.
4. If credentials were entered, revoke sessions, reset the password, review authentication methods, and investigate follow-on access.
5. Preserve headers and investigation notes.
6. Notify the reporter and provide a short recognition lesson.

## Detection improvements

- detect sender and reply-to mismatches;
- monitor newly observed domains paired with credential-themed URLs;
- correlate reported messages with risky sign-ins;
- prioritize messages targeting privileged or finance identities; and
- avoid treating display-name similarity alone as a definitive verdict.

## Safety note

No live malicious URL, attachment, credential, or victim information is included.
