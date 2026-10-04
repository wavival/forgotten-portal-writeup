# Forgotten Portal Roadmap

> Last updated: 2026-10-04

What is pending in the reports and notes. The writeup and the notes already agree on seven findings (see `notes/writeup.md`).

## Reports (PDF, no source files in the repository)

Both reports carry inconsistencies. Fixing them needs the editable sources, which are not in the repository: add the sources, or regenerate the PDFs.

- [ ] Technical report, executive summary: says "four Critical-severity findings". Its findings table and the executive report say three.
- [ ] FINDING-07 has CVSS 8.8 and is labelled Critical. CVSS v3.1 rates 7.0 to 8.9 as High. Either change the label or the score.
- [ ] Risk matrix (both reports): likelihood and impact are swapped for F01, F03, F05 and F07 against the values in each finding.
- [ ] Remediation timelines: the technical report says 0 to 7 days (Critical) and 0 to 14 days (High); the executive report says 0 to 30 days for Critical and 30 to 90 days for High, while its legend says High is 30 days.
- [ ] Technical report, FINDING-04: the title says "Publicly Readable Log File" and the description says it is readable by the `www-data` account. Align the wording.
- [ ] Organization name: the reports say "EAFIT University"; the README and the writeup say "Nodo EAFIT, cybersecurity accelerator".

## MITRE ATT&CK mapping

These need the author's judgement on the technique, so they are not changed yet.

- [ ] Technical report: T1548.003 is named "Sudo Enumeration" under Discovery. T1548.003 is "Sudo and Sudo Caching" (privilege escalation).
- [ ] Netcat reverse shell over TCP 443 is mapped to T1071.001 (Web Protocols). Raw TCP fits T1095 (Non-Application Layer Protocol) better; the payload transfer over HTTP fits T1105 (Ingress Tool Transfer).
- [ ] `notes/mitre-attack-mapping.md` and the report table do not list the same techniques. Make one the source and generate the other.

## Repository

- [x] Renamed `notes/mittre-attack-mapping.md` to `notes/mitre-attack-mapping.md` and updated the README link. The blog post could not be checked from this environment.
- [ ] Add the report sources (and a build step) so the PDFs can be regenerated.
- [ ] Add a CHANGELOG once the reports change.
