# Forgotten Portal | Pentest Writeup.

Full penetration test documentation for the **Forgotten_Portal** machine
from [DockerLabs](https://dockerlabs.es), developed as part of the
cybersecurity accelerator at Nodo EAFIT (2026).

## Attack Summary.

1. Sensitive data exposed in HTML source code → revealed hidden upload page
2. File upload form accepting `.php` → Remote Code Execution via web shell
3. Credentials stored in Base64 inside access log → lateral movement to alice
4. Shared RSA key across all system users → lateral movement to bob
5. Misconfigured sudo permissions on `tar` → privilege escalation to root

**Result:** Full system compromise without credentials or advanced exploits.

## Tools Used.

`nmap` · `gobuster` · `netcat` · `python3` · `base64` · `GTFOBins`

## Repository Structure.
 
```
forgotten-portal-writeup/
├── evidence/                    # 28 annotated screenshots, full attack chain.
├── notes/
│   ├── writeup.md               # Step-by-step technical walkthrough with images.
│   └── mitre-attack-mapping.md  # Full MITRE ATT&CK TTP mapping.
└── reports/
    └── technical-report.pdf     # Full technical report (Spanish).
```
## Writeup.

Step-by-step walkthrough with screenshots: [notes/writeup.md](notes/writeup.md)

Full narrative on the Lúmina W blog.
[Read here.](https://blog.luminaw.co/blog/forgotten-portal-pentest-dockerlabs)

## Methodology.

PTES (Penetration Testing Execution Standard) · MITRE ATT&CK mapping included

---

*Developed in a controlled environment for academic purposes.
No real systems were affected.*