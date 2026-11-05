# NS-004 — Final Investigation Report

**Organisation:** Northstar Services  
**Case date:** 26 October 2026  
**Severity:** HIGH  
**Status:** OPEN  
**Analyst:** Nwobodo Chukwuemeka Victor  
**Report version:** 1.0 — 1 November 2026  
**Briefing link:** [Insert recorded three-minute briefing link before submission]

> Fictional training case. This report is based on the supplied NS-004 case dossier and its embedded evidence summaries. No independent raw-log acquisition or analysis was performed.

## 1. Executive summary
On 26 October 2026, a suspicious email reached Maya at Northstar Services and requested her existing company password. The displayed portal text did not match the actual destination hostname, which ended in `billing-check.example`. Endpoint and network records support that NS-LT-12 connected to the suspicious destination, but the TLS content was not decrypted and credential submission is not confirmed.

At 09:07 UTC, Maya's account successfully signed in from unfamiliar source IP `198.51.100.44`, creating session `S-404`. That session successfully read `billing-register.csv` twice, with 40,960 bytes recorded for each read; an attempt to read `payroll.csv` was denied. The recorded return values total 81,920 bytes, but this is not a confirmed total of data exfiltrated.

Severity is High under the case rules because a suspicious successful session accessed sensitive business records. S-404 was revoked at 09:40 UTC, and a later access request was denied. The case remains open because endpoint collection, user interview, full session-history review, OAuth grant review, and data-scope assessment are pending. Attacker identity, malware execution, complete exfiltration scope, and a breach-notification decision are not established.

## 2. Scope, authority, and evidence preservation
The junior analyst was authorised only to examine supplied copies, document findings, and recommend actions. No account changes, session revocation, endpoint isolation, external contact, or restoration were performed by the junior analyst.

Preservation requirements:
- Preserve supplied evidence and exports without editing; analyse copies.
- Record filename, source, collector, collection time and time zone, SHA-256 digest, verification result, and every transfer/recipient.
- A matching SHA-256 digest supports byte consistency with a reference digest; it does not independently prove authenticity or completeness.
- Request authorised collection of NS-LT-12 endpoint evidence before reboot or wipe. D01 authorised collection but did not authorise a wipe or rebuild.

The raw CSV templates, full forensic acquisition packages, collection receipts, and hash manifest were not available for independent verification. Collector, collection time, SHA-256 values, and custody details are therefore not claimed.

## 3. Email and baseline analysis
### E01 — suspicious message
- Display name: Northstar Helpdesk.
- From: `help@billing-check.example`; Reply-To: `review@billing-check.example`.
- Trusted gateway results: SPF, DKIM, and DMARC passed for `billing-check.example`.
- Displayed URL: `https://portal.northstar.example`.
- Actual hostname: `portal.northstar.example.billing-check.example`.
- The body asks Maya to provide her existing company password.
- Attachment: `billing-update.pdf.html`, content type `text/html`; attachment bytes were not supplied.

Passing email authentication establishes authentication for the sending domain, not Northstar affiliation or safe content. The actual hostname ends in `billing-check.example`. These are strong phishing indicators. Whether Maya entered or submitted credentials is not confirmed.

### E02 — control message
The control email came from the approved `northstar.example` domain, directed the user to an already-saved portal bookmark, and had no attachment. It provides a useful contrast with E01.

### Endpoint comparison
P03 records an unusual-process alert for `invoiceviewer.exe` on NS-LT-12. This is an alert requiring validation, not proof of malware. P04 records an approved `approved-agent.exe` update under CHG-404 on NS-LT-14, a different device. It does not establish an approved update on NS-LT-12.

## 4. Timeline
All times are UTC unless stated. WAT = UTC+01:00. NS-LT-12 was 120 seconds fast. For P01–P03: corrected UTC = original endpoint time minus 120 seconds; WAT = corrected UTC plus one hour. Other clocks are treated as accurate.

| Evidence | Recorded UTC | Corrected UTC | WAT | Observation |
|---|---:|---:|---:|---|
| E02 | 08:50 | 08:50 | 09:50 | Control email; approved domain and saved-bookmark guidance. |
| I01 | 08:58 | 08:58 | 09:58 | Maya MFA sign-in success from normal office egress; S-OFFICE. |
| E01 | 09:00 | 09:00 | 10:00 | Password request, deceptive hostname, HTML attachment. |
| P01 | 09:04 original | 09:02 | 10:02 | NS-LT-12 saved billing-update.pdf.html. |
| N01 | 09:02:55 | 09:02:55 | 10:02:55 | DNS query to deceptive hostname; answer 198.51.100.60. |
| P02 | 09:05 original | 09:03 | 10:03 | NS-LT-12 browser connection to suspicious host on 443. |
| N02 | 09:03 | 09:03 | 10:03 | TLS connection to 198.51.100.60; not decrypted. |
| P03 | 09:06 original | 09:04 | 10:04 | invoiceviewer.exe unusual-process alert. |
| N03 | 09:04 | 09:04 | 10:04 | Separate HTTP GET /version to updates.northstar.example; 200. |
| I02 | 09:06 | 09:06 | 10:06 | Maya password sign-in failed from 198.51.100.44; no session. |
| I03 | 09:07 | 09:07 | 10:07 | Maya password sign-in succeeded from 198.51.100.44; creates S-404. |
| C01 | 09:08 | 09:08 | 10:08 | S-404 successfully read billing-register.csv; 40,960 bytes. |
| C02 | 09:09 | 09:09 | 10:09 | S-404 payroll.csv request denied; 0 bytes. |
| I04 | 09:20 | 09:20 | 10:20 | Maya password changed from office session S-OFFICE. |
| C03 | 09:25 | 09:25 | 10:25 | S-404 successfully read billing-register.csv again; 40,960 bytes. |
| D01 | 09:30 | 09:30 | 10:30 | Incident lead approves S-404 revocation and endpoint evidence collection; no wipe/rebuild. |
| B02 | 09:35 | 09:35 | 10:35 | Online snapshot; integrity unverified; no restore test. |
| I05 | 09:40 | 09:40 | 10:40 | Identity administrator successfully revokes S-404. |
| C04 | 09:41 | 09:41 | 10:41 | S-404 billing-register.csv request denied; 0 bytes. |
| D02 | 09:42 | 09:42 | 10:42 | Revocation confirmed; monitor new sessions and review sessions/OAuth. |
| D03 | 09:45 | 09:45 | 10:45 | Endpoint collection, interview, session history, OAuth review, and scope assessment pending; case open. |

## 5. Evidence correlation
- P02's original 09:05 UTC time becomes 09:03 UTC after clock correction, matching N02.
- P02 and N02 match on source `10.40.0.12`, destination `198.51.100.60`, and hostname. N01's DNS answer matches N02's destination.
- I03 creates S-404, which appears in C01, C02, and C03.
- C03 occurred after I04, showing that the password change did not revoke S-404.
- The sequence is an observed progression, not proof that E01 caused every later event.

TLS content was not decrypted. Credential submission and data upload through N02 cannot be confirmed. N03 is separate traffic and should not be conflated with N02.

## 6. Findings and impact
1. **Phishing indicators:** E01 requested an existing password and used a deceptive hostname under `billing-check.example`.
2. **Endpoint/network contact:** P02 and N02 support a connection to the deceptive hostname after clock correction.
3. **Suspicious successful sign-in:** I03 records a successful sign-in from unfamiliar IP `198.51.100.44`, creating S-404. The IP does not identify a person or location.
4. **Sensitive billing access:** C01 and C03 show two successful reads of `billing-register.csv`, each returning 40,960 bytes. Their recorded return values total 81,920 bytes; this is not confirmed exfiltration.
5. **Payroll request denied:** C02 shows `payroll.csv` denied with zero bytes returned. No successful payroll access is shown in the supplied records.
6. **Session persisted after password change:** C03 occurred after the 09:20 password change. A password change does not automatically revoke an existing session under the case policy.
7. **Revocation:** S-404 was revoked at 09:40 UTC. C04 is one later denied request, not proof of complete eradication.

## 7. Severity assessment
**Severity: HIGH.** The exercise rules classify suspicious successful access to sensitive business records as High severity. The successful `billing-register.csv` reads through S-404 meet that rule. This is a training-case severity assessment, not a legal breach determination.

Not established: whether Maya submitted her password; whether invoiceviewer.exe was malicious or the attachment executed; TLS content or upload; complete exposure scope; successful payroll access; theft of every company file; file corruption or ransomware; attacker identity; malicious OAuth grant; complete eradication; or whether breach notification is required.

## 8. Containment and escalation
D01 records the incident lead's approval to revoke S-404 and collect endpoint evidence. I05 records successful revocation at 09:40 UTC, and D02 confirms it. The junior analyst did not execute containment.

Next steps:
- Maintain High-severity oversight under the incident lead.
- Review all related sessions and subsequent sign-ins.
- Obtain full session history and OAuth grant records; no OAuth export was supplied, so a malicious grant must not be assumed.
- Collect NS-LT-12 endpoint evidence through authorised personnel, preserving evidence before reboot or wipe.
- Interview Maya through the approved process.
- Obtain complete application audit records to assess access scope.
- Continue monitoring new sessions.

## 9. Recovery and monitoring
Restoration is not currently justified by the supplied evidence: no file corruption or ransomware is demonstrated.

B01 is the stronger candidate for further clean-recovery assessment if restoration becomes necessary: immutable offline backup created 25 October at 23:00 UTC, integrity verified, isolated restore test passed 26 October at 07:00 UTC, and no evidence of access by S-404.

B02 is weaker: online snapshot created 26 October at 09:35 UTC after suspicious activity began, integrity unverified, and no restore test recorded.

B01 is not an instruction to restore production. Before restoration, the incident lead should confirm a clean recovery point, the data owner should validate the data, and authorised staff should test in isolation with monitoring and a rollback plan.

## 10. Open questions and handover
At D03 (09:45 UTC), the case remains OPEN. S-404 revocation is documented. Endpoint collection, user interview, full session history, OAuth review, and scope assessment remain pending. The next review owner is the incident lead. No breach-notification decision is recorded.

## 11. Final assessment
The supplied evidence supports a High-severity incident involving suspicious account activity and successful access to sensitive billing records. The email contains strong phishing indicators, and endpoint/network records support a connection to the deceptive hostname. Session S-404 was revoked, but the full exposure scope and complete eradication remain unverified. Further authorised evidence collection and review are required before the case can be closed or any notification or recovery decision can be made.
