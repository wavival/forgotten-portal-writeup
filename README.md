<h1 align="left">
  <img src="assets/icon.png" width="48px" valign="middle">
  Forgotten Portal • Penetration testing
</h1>

![Banner principal](assets/banner-main.png)

[![Writeup](https://img.shields.io/badge/Writeup-blog.luminaw.co-407bff?style=for-the-badge&logo=hashnode&logoColor=white)](https://blog.luminaw.co/forgotten-portal-pentesting-dockerlabs/)
[![Portfolio](https://img.shields.io/badge/Portfolio-wavival.dev-407bff?style=for-the-badge&logo=vercel&logoColor=white)](https://wavival.dev)

> Full penetration testing documentation for the **Forgotten_Portal** machine from [DockerLabs](https://dockerlabs.es), developed as part of the cybersecurity accelerator at Nodo EAFIT (2026).

## Table of Contents

- [Overview](#overview)
- [Attack Chain](#attack-chain--forgotten-portal)
- [Reports](#reports--technical--executive)
- [Evidence](#evidence--full-capture-walkthrough)
- [License](#license)
- [Contact](#contact)

## Overview

Forgotten_Portal is a DockerLabs Linux machine that demonstrates an end-to-end compromise through exposed information, unrestricted file upload, credential exposure, shared SSH keys, and an insecure sudo configuration. The assessment documents reconnaissance, exploitation, lateral movement, and privilege escalation to `root`.

For the expanded walkthrough, including commands, screenshots, findings, and remediation context, read the published [Forgotten Portal penetration-testing writeup](https://blog.luminaw.co/forgotten-portal-pentesting-dockerlabs/).

## Attack Chain • Forgotten Portal

End-to-end penetration test of a vulnerable Docker-based machine. Full kill chain from zero to root: reconnaissance, enumeration, vulnerability exploitation, and privilege escalation, achieving full system compromise without credentials or advanced exploits.

1. Sensitive data exposed in HTML source code → revealed hidden upload page
2. File upload form accepting `.php` → Remote Code Execution via web shell
3. Credentials stored in Base64 inside access log → lateral movement to `alice`
4. Shared RSA key across all system users, plus its passphrase written in plain text in an internal incident report → lateral movement to `bob`
5. Misconfigured sudo permissions on `tar` → privilege escalation to `root`

[Writeup](https://blog.luminaw.co/forgotten-portal-pentesting-dockerlabs/) • [Laboratory](https://dockerlabs.es)

Used tools: `NMAP` `Gobuster` `Netcat` `Python` `Base64` `GTFOBins` `MITRE ATT&CK` `PTES` `DockerLabs` `Linux`

![Banner Forgotten Portal Machine](assets/banner-forgotten-portal.png)

## Reports • Technical & Executive

Two deliverables aligned to different audiences: a technical report documenting every step, payload, and finding for security teams, plus an executive report translating impact and remediation priorities for non-technical stakeholders.

Methodology follows PTES (Penetration Testing Execution Standard) with findings mapped to the MITRE ATT&CK framework. The technical report lists seven findings (three Critical, two High, two Medium); the [writeup](notes/writeup.md) lists the same seven with their CWE classification.

[Technical Report](reports/technical-report.pdf) • [Executive Report](reports/executive-report.pdf) • [MITRE ATT&CK Mapping](notes/mitre-attack-mapping.md)

Used tools: `PTES` `MITRE ATT&CK` `Markdown` `PDF`

![Banner Reports](assets/banner-reports.png)

## Evidence • Full Capture Walkthrough

28 annotated screenshots covering the full attack chain, from initial machine deployment and network discovery to web shell upload, lateral movement across users, and root flag capture. Each step is reproducible and tied to the technical report.

Repository structure:

```
forgotten-portal-writeup/
├── evidence/                       # 28 annotated screenshots, full attack chain.
├── docs/
│   └── ROADMAP.md                  # Pending work on the reports and notes.
├── notes/
│   ├── writeup.md                  # Step-by-step technical walkthrough with images.
│   └── mitre-attack-mapping.md     # Full MITRE ATT&CK TTP mapping.
└── reports/
    ├── technical-report.pdf        # Full technical report (English).
    └── executive-report.pdf        # Executive summary for non-technical stakeholders (English).
```

[Evidence folder](evidence/) • [Step-by-step writeup](notes/writeup.md)

Used tools: `Linux` `Bash` `Markdown` `Screenshots`

![Banner Evidence](assets/banner-evidence.png)

## License

Released under the MIT License. Free to use, modify, and redistribute with attribution. Full terms in [LICENSE](LICENSE).

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

## Contact

<img src="assets/logo-w.png" width="48px" alt="wavival.dev">

> One click away

### Your next idea deserves code that can sustain it.

I design and build complete products, from the backend to interfaces your users love. With AI integration and security by design.

Projects start at COP 2,000,000 / USD 500 depending on scope (MVPs from 3 to 6 weeks). Limited availability, replies within 24 hours.

[Build my product](https://www.wavival.dev/contacto) • [View services](https://www.wavival.dev/servicios)

Full Stack Developer. Security integrated. AI applied. Products that scale.
