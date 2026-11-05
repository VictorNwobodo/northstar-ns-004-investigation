# Evidence Correlation — NS-004

## Email to endpoint/network
E01 requested Maya's existing company password and displayed a portal URL whose actual hostname was `portal.northstar.example.billing-check.example`. P01 records the HTML attachment being saved on NS-LT-12. P02 records a browser connection to that hostname. After correcting NS-LT-12's clock, P02 aligns with N02 at 09:03 UTC. N01's DNS answer (198.51.100.60) matches N02's destination.

**Limit:** TLS content was not decrypted. Credential submission and data upload are not confirmed. The sequence does not prove E01 caused every later event.

## Identity to application
I03 records a successful sign-in from 198.51.100.44 and creates session S-404. C01, C02, and C03 are associated with S-404. C01 and C03 show successful reads of billing-register.csv, each returning 40,960 bytes. C02 shows payroll.csv denied with zero bytes.

I04 records a password change at 09:20 UTC. C03 occurs at 09:25 UTC through S-404, demonstrating that the password change did not automatically revoke the existing session.

## Revocation to later activity
I05 records successful revocation of S-404 at 09:40 UTC. C04 at 09:41 UTC records a denied billing-register.csv request. One denied request does not prove all sessions, tokens, access paths, or systems are clear.

## Separate and unconfirmed activity
N03 is separate HTTP traffic to updates.northstar.example and must not be merged with N02. P03 is an unusual-process alert, not proof of malware. P04 is an approved update on NS-LT-14, not NS-LT-12. The unfamiliar IP does not identify an attacker or physical location.