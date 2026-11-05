# Incident Timeline — NS-004

All times are UTC unless stated. WAT = UTC+01:00. NS-LT-12 was 120 seconds fast. Correct P01–P03 by subtracting 120 seconds from their original endpoint timestamps. Other clocks are treated as accurate.

| Evidence | Corrected UTC | WAT | Event |
|---|---:|---:|---|
| E02 | 08:50 | 09:50 | Approved control email received. |
| I01 | 08:58 | 09:58 | Maya MFA sign-in success from normal office egress; S-OFFICE. |
| E01 | 09:00 | 10:00 | Suspicious password-request email received. |
| P01 | 09:02 | 10:02 | NS-LT-12 saved HTML attachment. |
| N01 | 09:02:55 | 10:02:55 | DNS query; answer 198.51.100.60. |
| P02 / N02 | 09:03 | 10:03 | Endpoint and network records support connection to deceptive hostname over TLS. |
| P03 | 09:04 | 10:04 | Unusual-process alert for invoiceviewer.exe. |
| N03 | 09:04 | 10:04 | Separate HTTP GET /version to updates.northstar.example; 200. |
| I02 | 09:06 | 10:06 | Password sign-in failure from 198.51.100.44; no session. |
| I03 | 09:07 | 10:07 | Password sign-in success from 198.51.100.44; creates S-404. |
| C01 | 09:08 | 10:08 | Successful billing-register.csv read; 40,960 bytes. |
| C02 | 09:09 | 10:09 | payroll.csv read denied; 0 bytes. |
| I04 | 09:20 | 10:20 | Password changed from office session. |
| C03 | 09:25 | 10:25 | Successful billing-register.csv read through S-404; 40,960 bytes. |
| D01 | 09:30 | 10:30 | Incident lead approves S-404 revocation and endpoint collection. |
| B02 | 09:35 | 10:35 | Online snapshot; integrity unverified. |
| I05 | 09:40 | 10:40 | S-404 successfully revoked. |
| C04 | 09:41 | 10:41 | Later billing-register.csv request denied; 0 bytes. |
| D02 | 09:42 | 10:42 | Revocation confirmed; monitoring and session/OAuth review directed. |
| D03 | 09:45 | 10:45 | Case remains open; additional collection and review pending. |

## Clock correction
P01: 09:04 original UTC → 09:02 corrected UTC → 10:02 WAT.  
P02: 09:05 original UTC → 09:03 corrected UTC → 10:03 WAT.  
P03: 09:06 original UTC → 09:04 corrected UTC → 10:04 WAT.

P02 and N02 align at 09:03 UTC after correction. Their source, destination, and hostname also match.