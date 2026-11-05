# NS-004 — Three-Minute Briefing Notes

These notes align with the 10-slide presentation. Add the recorded briefing link to the final report before submission.

1. **Cover:** Good day. My name is Victor, and I'm a Junior SOC Analyst. Today, I'll present my investigation of case NS-004, involving a suspected account compromise at Northstar Services.
2. **At a glance:** The investigation took place on 26 October 2026. I examined the supplied evidence to understand what happened, what data was accessed, and what actions were taken.
3. **Email:** The investigation started with an email claiming to be from Northstar Helpdesk. It asked Maya for her existing company password. The link looked legitimate, but the actual website address belonged to a different domain. This was a strong sign of phishing.
4. **Clock correction:** Next, I checked the activity on Maya's computer. Its clock was two minutes fast, so I corrected the timestamps. After correcting them, the computer's connection matched the network record.
5. **Network:** The network records confirmed a connection to the suspicious website. However, I could not see the encrypted content, so I cannot confirm whether Maya's password was sent.
6. **Identity:** At 09:07 UTC, Maya's account successfully signed in from an unfamiliar IP address. This created session S-404. That session accessed a billing file, even after Maya changed her password.
7. **Impact:** The billing file was accessed successfully twice. However, an attempt to access the payroll file was denied. Because the billing file contained customer information and invoice amounts, I classified the incident as High severity. The full extent of data exposure is still unknown.
8. **Containment:** The incident lead approved the session revocation, and the identity administrator completed it. A later access attempt was denied. However, more investigation is needed before we can confirm that all suspicious activity has stopped.
9. **Next steps:** I recommend collecting more evidence from the computer, reviewing other sessions, checking OAuth access, and interviewing Maya. If recovery becomes necessary, backup B01 is the better candidate for further assessment.
10. **Conclusion:** In conclusion, the evidence shows suspicious account activity and successful access to billing data. The session was revoked, but the full impact is still unknown. The case remains open for further investigation. Thank you.