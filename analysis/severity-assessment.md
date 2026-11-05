# Severity Assessment — NS-004

**Assigned severity: HIGH**

The exercise rubric defines High severity as suspicious successful access to sensitive business records or credible ongoing account misuse requiring immediate lead review.

## Evidence supporting High
- I03: Maya's account successfully signs in from unfamiliar IP 198.51.100.44 and creates S-404.
- C01: S-404 successfully reads billing-register.csv; 40,960 bytes returned.
- C03: S-404 successfully reads the same file again; 40,960 bytes returned.
- The billing register contains customer contact information and invoice amounts.

The two recorded return values total 81,920 bytes. This is not confirmed total exfiltration or proof of what was retained.

## Limiting and counter-evidence
- C02: payroll.csv request denied; zero bytes returned.
- C04: later billing-register.csv request denied after S-404 revocation.
- No evidence establishes successful payroll access or theft of every company file.
- The unfamiliar IP does not identify a person or location.
- TLS payload is unavailable; credential transmission is not confirmed.
- P03 requires validation and is not proof of malware.

This is a training-case severity assessment, not a legal breach determination or breach-notification decision.