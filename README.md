<h1 align="left">
  <img src="assets/icon.png" width="48px" valign="middle">
  Forgotten Portal • Penetration testing
</h1>

![Banner principal](assets/banner-main.png)

[![Writeup](https://img.shields.io/badge/Writeup-blog.luminaw.co-407bff?style=for-the-badge&logo=hashnode&logoColor=white)](https://blog.luminaw.co/forgotten-portal-pentesting-dockerlabs/)
[![Portfolio](https://img.shields.io/badge/Portfolio-wavival.dev-407bff?style=for-the-badge&logo=vercel&logoColor=white)](https://wavival.dev)

> Full penetration testing documentation for the **Forgotten_Portal** machine from [DockerLabs](https://dockerlabs.es), developed as part of the cybersecurity accelerator at Nodo EAFIT (2026).

## Attack Chain • Forgotten Portal

End-to-end penetration test of a vulnerable Docker-based machine. Full kill chain from zero to root: reconnaissance, enumeration, vulnerability exploitation, and privilege escalation, achieving full system compromise without credentials or advanced exploits.

1. Sensitive data exposed in HTML source code → revealed hidden upload page
2. File upload form accepting `.php` → Remote Code Execution via web shell
3. Credentials stored in Base64 inside access log → lateral movement to `alice`
4. Shared RSA key across all system users → lateral movement to `bob`
5. Misconfigured sudo permissions on `tar` → privilege escalation to `root`

[Writeup](https://blog.luminaw.co/forgotten-portal-pentesting-dockerlabs/) • [Laboratory](https://dockerlabs.es)

Used tools: `NMAP` `Gobuster` `Netcat` `Python` `Base64` `GTFOBins` `MITRE ATT&CK` `PTES` `DockerLabs` `Linux`

![Banner Forgotten Portal Machine](assets/banner-forgotten-portal.png)

## Reports • Technical & Executive

Two deliverables aligned to different audiences: a technical report documenting every step, payload, and finding for security teams, plus an executive report translating impact and remediation priorities for non-technical stakeholders.

Methodology follows PTES (Penetration Testing Execution Standard) with findings mapped to the MITRE ATT&CK framework.

[Technical Report](reports/technical-report.pdf) • [Executive Report](reports/executive-report.pdf) • [MITRE ATT&CK Mapping](notes/mittre-attack-mapping.md)

Used tools: `PTES` `MITRE ATT&CK` `Markdown` `PDF`

![Banner Reports](assets/banner-reports.png)

## Evidence • Full Capture Walkthrough

28 annotated screenshots covering the full attack chain, from initial machine deployment and network discovery to web shell upload, lateral movement across users, and root flag capture. Each step is reproducible and tied to the technical report.

Repository structure:

```
forgotten-portal-writeup/
├── evidence/                       # 28 annotated screenshots, full attack chain.
├── notes/
│   ├── writeup.md                  # Step-by-step technical walkthrough with images.
│   └── mittre-attack-mapping.md    # Full MITRE ATT&CK TTP mapping.
└── reports/
    ├── technical-report.pdf        # Full technical report (Spanish).
    └── executive-report.pdf        # Executive summary for non-technical stakeholders.
```

[Evidence folder](evidence/) • [Step-by-step writeup](notes/writeup.md)

Used tools: `Linux` `Bash` `Markdown` `Screenshots`

![Banner Evidence](assets/banner-evidence.png)

## License

Released under the MIT License. Free to use, modify, and redistribute with attribution. Full terms in [LICENSE](LICENSE).

## Contact

![Banner footer](assets/banner-footer.png)

<h3 align="left">
  <img src="assets/logo-w.png" width="48px" valign="middle">
  Valentina Ramírez • @wavival
</h3>

> Thanks for getting here. Let's build great things.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-wavival-407bff?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/wavival)
[![Instagram](https://img.shields.io/badge/Instagram-@wavival-407bff?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/wavival)
[![Email](https://img.shields.io/badge/Email-wavival.dev@luminaw.co-407bff?style=for-the-badge&logo=gmail&logoColor=white)](mailto:wavival.dev@luminaw.co)
