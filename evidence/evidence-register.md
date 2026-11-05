# Evidence Register — NS-004

**Evidence window:** 26 October 2026, 08:50–09:45 UTC  
**Handling:** Supplied evidence summaries only; raw underlying exports were not independently acquired or validated.

| Category | Evidence IDs | Records support | Limitation |
|---|---|---|---|
| Email | E01–E02 | Suspicious message and approved control message | Full raw message and attachment bytes unavailable. |
| Endpoint | P01–P04 | File save, browser connection, process alert, approved-change comparison | Selected events only; no full disk image or complete process/file history. |
| Network | N01–N03 | DNS answer, TLS connection, separate HTTP request | Selected records only; no complete PCAP or TLS decryption keys. |
| Identity | I01–I05 | Sign-ins, password change, session revocation | Full session/token history not supplied. |
| Application audit | C01–C04 | Successful and denied file reads | Complete application audit and total exposure scope unavailable. |
| Decisions | D01–D03 | Approval, revocation confirmation, pending tasks | Decision summaries supplied. |
| Backups | B01–B02 | Backup integrity and restore-test comparison | No restoration ordered. |

## Preservation record
The supplied material does not include independently verifiable collector names, acquisition timestamps, SHA-256 values, verification receipts, or transfer history. Do not populate these fields with invented values.

For any additional authorised collection, record the evidence item and filename, original source/host and collection method, collector identity and authority, collection timestamp and time zone, SHA-256 digest and verification result, original/copy designation and storage location, and every transfer, recipient, and timestamp.

A matching SHA-256 digest supports byte consistency with a reference digest; it does not independently establish authenticity or completeness.