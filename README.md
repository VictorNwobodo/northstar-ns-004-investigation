# Northstar Services — Case NS-004

**Case type:** Suspected phishing-led account compromise  
**Severity:** High  
**Status:** Open — further investigation required  
**Evidence window:** 26 October 2026, 08:50–09:45 UTC  
**Analyst role:** Junior SOC Analyst

## Overview

This repository documents a fictional SOC investigation into suspicious activity involving Maya's Northstar Services account. The supplied evidence shows a deceptive email, a connection to a misleading hostname, a successful sign-in from an unfamiliar IP address, and successful reads of a billing register using session `S-404`.

The incident lead approved revocation of `S-404`; the identity administrator completed it at 09:40 UTC. The case remains open because endpoint collection, broader session review, user confirmation, and impact assessment are still pending.

## Key findings

- An email claiming to be Northstar Helpdesk asked Maya to provide her existing company password.
- The displayed URL concealed the actual hostname: `portal.northstar.example.billing-check.example`.
- Endpoint clock correction aligns P02 with network event N02 at 09:03 UTC.
- Maya's account successfully authenticated from `198.51.100.44`, creating session `S-404`.
- `S-404` successfully read `billing-register.csv` twice, with 81,920 recorded bytes returned in total.
- An attempt to read `payroll.csv` was denied. The supplied records do not establish payroll access.
- TLS content was not decrypted; credential submission and data exfiltration cannot be confirmed.

## Repository contents

- `report/` — final investigation report in Markdown.
- `analysis/` — timeline, evidence correlation, severity assessment, and handover recommendations.
- `presentation/` — three-minute briefing script aligned with the report.
- `evidence/` — evidence register and limitations.

## Important limitations

This is a fictional teaching case. The repository contains analyst documentation based on supplied evidence summaries, not raw production logs. The supplied evidence is selective. No full disk image, packet capture, raw email/attachment bytes, TLS decryption keys, complete token history, user interview, VPN inventory, or post-09:45 UTC logs were provided.

The unfamiliar IP address does not establish an individual's identity or physical location. A successful TLS connection does not prove that credentials were submitted or data was uploaded. Hash equality, if recorded by an evidence custodian, supports byte consistency and does not independently prove authenticity.

## Handling and scope

The junior analyst's authority is limited to examining supplied copies, documenting findings, and recommending actions. This repository does not claim that the junior analyst performed containment, account resets, endpoint isolation, or system restoration.

All timestamps ending in `Z` are UTC. WAT is UTC+01:00. The NS-LT-12 clock was two minutes fast; its timestamps are corrected by subtracting two minutes before conversion to WAT.

## Disclaimer

All organisations, people, domains, IP addresses, hostnames, events, and records in this case are fictional or reserved for documentation/training use. Do not treat the example indicators as live threat intelligence or scan them. This case study is for learning and portfolio demonstration only.
