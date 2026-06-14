# Jeremy Lim | Cybersecurity Portfolio

## About Me

Career transitioner into cybersecurity, targeting **SOC Analyst / Cybersecurity Analyst** roles.

~8 years in F&B operations — including internal IT support and incident handling for a 20-person business — now focused on **blue-team detection and SIEM work**. CEH and Splunk SCDA certified, currently building a GCP detection-engineering homelab and working through the TryHackMe SOC Level 1 path.

🔗 [LinkedIn](https://linkedin.com/in/jeremy-lzh) · [GitHub](https://github.com/z1r0h)

---

## Certifications

- **CEH** (Certified Ethical Hacker) — April 2026
- **Splunk SCDA** (SPLK-5001) — May 2026
- **TryHackMe — Cyber Security 101 (SEC1)** — May 2026
- **TryHackMe — SOC Level 1 Path** — *In progress*

---

## Technical Skills

**Blue Team / SOC (focus)**
Splunk (SPL, dashboards, alert triage, event correlation), SIEM monitoring, log analysis, Sysmon telemetry, MITRE ATT&CK detection mapping, incident triage & documentation, escalation workflows

**Network & Traffic Analysis**
Wireshark, Nmap, firewall / log review, GCP VPC networking (subnets, firewall rules, IAP)

**Offensive (for detection context)**
Burp Suite, SQLi / XSS / CSRF, Hydra / John the Ripper / Hashcat, SUID privilege escalation, PHP reverse shell

**Reporting**
VAPT reports, CVSS scoring, CVE / CWE, MITRE ATT&CK, Cyber Kill Chain

---

## Projects

### SOC Detection Engineering Homelab (GCP) — *In progress*
**Repo:** [github.com/z1r0h/GCP-Homelab](https://github.com/z1r0h/GCP-Homelab)

A self-built detection lab on Google Cloud for simulating attacks and writing the matching detections in Splunk.

- 4-VM private VPC (Windows DC, Windows client, Splunk Enterprise, Kali Linux); custom Kali image, IAP tunnelling, no public IPs
- Telemetry pipeline: Sysmon (SwiftOnSecurity) → Universal Forwarder → Splunk Enterprise
- Currently building MITRE ATT&CK detections, starting with **Network Scanning (T1046)** — authoring/tuning the SPL and investigating Sysmon network-connection (Event ID 3) visibility for SYN scans

### Capstone VAPT — Mr. Robot (TryHackMe)
**Repo:** [github.com/z1r0h/Cybersecurity-Portfolio](https://github.com/z1r0h/Cybersecurity-Portfolio)

- Full attack chain: Recon → Enumeration → Initial Access → Privilege Escalation
- WordPress exploitation for initial foothold, SUID binary abuse for privilege escalation
- Documented findings with CVSS ratings and detection notes for endpoint and web access logs
- Tools: Nmap, Gobuster, Hydra, PHP reverse shell

---

## Education

- **Professional Certificate in Cybersecurity** — MAGES Institute of Excellence, Singapore | Oct 2025 – Apr 2026
- **Higher Diploma in Business Management (Mandarin)** — EXERCEO Business International College
