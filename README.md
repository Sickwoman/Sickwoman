<div align="center">

<img src="profile/header.svg" width="860" alt="MOKSH VATSA · honeypots // network recon // open-source security // ML research" />

<br/>

<img src="https://img.shields.io/badge/OWASP_NETTACKER-CONTRIBUTOR-000000?style=flat-square&labelColor=0D1024&color=A78BFA" alt="OWASP Nettacker contributor" />
<img src="https://img.shields.io/badge/HONEYNET_OCHI-CONTRIBUTOR-000000?style=flat-square&labelColor=0D1024&color=60A5FA" alt="honeynet/ochi contributor" />
<img src="https://img.shields.io/badge/BASED_IN-INDIA-000000?style=flat-square&labelColor=0D1024&color=4338CA" alt="Based in India" />
<img src="https://komarev.com/ghpvc/?username=Sickwoman&color=a78bfa&style=flat-square&label=VISITORS+LOGGED" alt="Profile views" />

<br/><br/>

<a href="#open-source-security">Open Source</a> ·
<a href="#changelog">Changelog</a> ·
<a href="#projects">Projects</a> ·
<a href="#arsenal">Arsenal</a>

</div>

Second-year student who builds traps for attackers and the tools that watch them. I run cloud
honeypots, write service-fingerprinting modules for **OWASP Nettacker**, and harden and extend
**The Honeynet Project's** ochi, the live UI for Glutton honeypot events. On the research side I
test ML claims against hard limits, from catching byzantine nodes in multi-party computation to
predicting antibiotic resistance across hospitals.

---

## Open Source Security

<img src="https://github.com/OWASP.png?size=80" width="32" height="32" align="middle" alt="" />&nbsp; **[OWASP/Nettacker](https://github.com/OWASP/Nettacker)** · automated penetration testing and vulnerability scanning framework &nbsp;<a href="https://github.com/OWASP/Nettacker/pulls?q=is%3Apr+is%3Amerged+author%3ASickwoman"><img src="https://img.shields.io/github/issues-search?query=repo%3AOWASP%2FNettacker%20is%3Apr%20is%3Amerged%20author%3ASickwoman&label=PRS%20MERGED&style=flat-square&labelColor=0D1024&color=A78BFA&logo=github&logoColor=white" align="middle" alt="PRs merged in OWASP Nettacker" /></a>

> **Version fingerprinting modules and port-scan coverage** · <sub>`#1832` · `#1878` · `#1890` · `Nov 2026`</sub>
>
> Wrote `grafana_version_scan` and `plex_version_scan`. Each reads the version from the service's
> unauthenticated endpoint (`/api/health`, `/identity`) and reports it as a fingerprint, with no CVE
> claim attached. Then fixed a coverage gap: port scan only probed Nmap's default port list, and with
> service discovery on, Nettacker drops every module whose port it didn't find. Modules on seven
> default ports never ran, including three CISA KEV checks (SonicWall SSL-VPN, Langflow, SmarterMail).
> Port scan now probes every module's default port.
>
> <sub>In review: `prometheus_version_scan` (#1930)</sub>

<img src="https://github.com/honeynet.png?size=80" width="32" height="32" align="middle" alt="" />&nbsp; **[honeynet/ochi](https://github.com/honeynet/ochi)** · The Honeynet Project's live UI for Glutton honeypot events &nbsp;<a href="https://github.com/honeynet/ochi/pulls?q=is%3Apr+is%3Amerged+author%3ASickwoman"><img src="https://img.shields.io/github/issues-search?query=repo%3Ahoneynet%2Fochi%20is%3Apr%20is%3Amerged%20author%3ASickwoman&label=PRS%20MERGED&style=flat-square&labelColor=0D1024&color=60A5FA&logo=github&logoColor=white" align="middle" alt="PRs merged in honeynet/ochi" /></a>

> **Authentication, sensor trust and CI hardening, plus query-language features** · <sub>`Oct – Nov 2026`</sub>
>
> Moved bearer auth onto `go-chi/jwtauth`, so a refused token now answers `401` instead of `500`
> (#167). Made the server reject events from unregistered sensors, checking the full sensor UUID
> rather than the 8-character display prefix, which would have been enough to impersonate one (#169).
> Gave the Actions workflows `permissions:` blocks, credential-free checkouts, timeouts and
> cancellation of superseded runs (#206). In the query DSL: `payload matches "<regex>"` (#219), plus
> scanner and transport filters (#194, #172).
>
> <sub>In review: generate secrets instead of shipping the default `jwt_secret` and `publish_token` (#237) · accept the publish token from a header, not just the URL (#201)</sub>

---

## Changelog

```diff
@@ sickwoman — recent activity @@
+ [2026-11]  OWASP/Nettacker · #1878 merged → plex_version_scan module
+ [2026-11]  OWASP/Nettacker · #1890 merged → port scan probes every module's default port
+ [2026-11]  honeypot-framework · #13 → Docker stack now turns Cowrie attacks into alerts, demo kit
+ [2026-11]  OWASP/Nettacker · #1832 merged → grafana_version_scan module
+ [2026-11]  honeynet/ochi · #219 merged → payload matches "<regex>" in the query DSL
+ [2026-10]  honeynet/ochi · #206 merged → hardened the GitHub Actions workflows
+ [2026-10]  honeynet/ochi · #169 merged → events from unregistered sensors rejected
+ [2026-10]  honeynet/ochi · #167 merged → bearer auth moved to go-chi/jwtauth
! [review]   OWASP/Nettacker #1930 · prometheus_version_scan
! [review]   honeynet/ochi #237 · generated secrets instead of shipped defaults
```

---

## Projects

<table>
<tr>
<td width="50%" valign="top">

### ❯ [MPC Node Threat Detection](https://github.com/Sickwoman/MPC-node-threat-detection)

A passive, share-free network monitor for multi-party computation. Over 100 real 3-party sessions it
catches dropped and duplicated messages with precision 1.00 and zero false positives, even under TLS.
It also maps the limit: a tampered Shamir share is statistically identical to an honest one, so
detection there is 0% and cryptographic malicious security has to take over.

`MPC` · `Network Monitoring` · `ML` · `Python`

</td>
<td width="50%" valign="top">

### ❯ [Antibiotic Resistance AI](https://github.com/Sickwoman/antibiotic-resistance-ai)

Research prototype that predicts antibiotic resistance from MALDI-TOF mass spectra (DRIAMS), focused
on whether models hold up across hospitals and over time. The frozen ciprofloxacin model was evaluated
once, under a pre-registration, on an independent hospital's public data. Not a clinical tool.

`ML Research` · `Generalization` · `Python`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### ❯ [Honeypot Framework](https://github.com/Sickwoman/honeypot-framework)

Cloud-native honeypot deployment: Cowrie SSH and OpenCanary decoys feeding an Elasticsearch, Logstash
and Kibana pipeline, with modular Terraform for multi-region AWS and an attack-simulation harness that
exercises the whole detection path locally.

`Honeypots` · `ELK` · `Terraform` · `AWS`

</td>
<td width="50%" valign="top">

### ❯ [SOC & Forensics Worklet Program](https://github.com/Sickwoman/soc-forensics-worklet-program)

A 12-week lab program in ten worklets, each built as documentation, a prototype and a working model:
pfSense with Snort, VLAN zero trust on VyOS, WireGuard, a Wazuh/ELK SIEM, OpenVAS, FreeIPA with MFA,
a ModSecurity WAF, then memory, disk and network forensics with Volatility 3, Autopsy and Wireshark.

`SOC` · `DFIR` · `Network Defense`

</td>
</tr>
</table>

**Also:**
[MAC Changer](https://github.com/Sickwoman/mac-changer-device-repo) (Kali, random MACs, timed rotation) ·
[Network Scanner](https://github.com/Sickwoman/network_scanner) ·
[Rust Learning](https://github.com/Sickwoman/Rust-learning-)

---

## Arsenal

```console
$ tree ~/arsenal
~/arsenal
├── honeypots/     Cowrie, OpenCanary, Glutton events, ELK pipelines, alerting
├── recon/         service fingerprinting, port scanning, OWASP Nettacker modules
├── appsec/        auth and token handling, secret defaults, CI / Actions hardening
├── ml-research/   scikit-learn, TensorFlow / Keras, generalization and calibration
└── infra/         Terraform, AWS, Docker, GitHub Actions
```

<p align="center">
<img src="https://img.shields.io/badge/Python-0D1024?style=flat-square&logo=python&logoColor=60A5FA" alt="Python" />
<img src="https://img.shields.io/badge/Go-0D1024?style=flat-square&logo=go&logoColor=60A5FA" alt="Go" />
<img src="https://img.shields.io/badge/C-0D1024?style=flat-square&logo=c&logoColor=60A5FA" alt="C" />
<img src="https://img.shields.io/badge/TypeScript-0D1024?style=flat-square&logo=typescript&logoColor=60A5FA" alt="TypeScript" />
<img src="https://img.shields.io/badge/Bash-0D1024?style=flat-square&logo=gnubash&logoColor=60A5FA" alt="Bash" />
<img src="https://img.shields.io/badge/HTML5-0D1024?style=flat-square&logo=html5&logoColor=60A5FA" alt="HTML5" />
<img src="https://img.shields.io/badge/Rust_(training)-A78BFA?style=flat-square&logo=rust&logoColor=0D1024" alt="Rust (training)" />
</p>
<p align="center">
<img src="https://img.shields.io/badge/Docker-0D1024?style=flat-square&logo=docker&logoColor=60A5FA" alt="Docker" />
<img src="https://img.shields.io/badge/Elastic-0D1024?style=flat-square&logo=elastic&logoColor=60A5FA" alt="Elastic" />
<img src="https://img.shields.io/badge/Kali-0D1024?style=flat-square&logo=kalilinux&logoColor=60A5FA" alt="Kali" />
<img src="https://img.shields.io/badge/Terraform-0D1024?style=flat-square&logo=terraform&logoColor=60A5FA" alt="Terraform" />
<img src="https://img.shields.io/badge/AWS-0D1024?style=flat-square&logo=amazonwebservices&logoColor=60A5FA" alt="AWS" />
<img src="https://img.shields.io/badge/Google_Cloud-0D1024?style=flat-square&logo=googlecloud&logoColor=60A5FA" alt="Google Cloud" />
<img src="https://img.shields.io/badge/GitHub_Actions-0D1024?style=flat-square&logo=githubactions&logoColor=60A5FA" alt="GitHub Actions" />
<img src="https://img.shields.io/badge/Git-0D1024?style=flat-square&logo=git&logoColor=60A5FA" alt="Git" />
</p>
<p align="center">
<img src="https://img.shields.io/badge/TensorFlow-0D1024?style=flat-square&logo=tensorflow&logoColor=60A5FA" alt="TensorFlow" />
<img src="https://img.shields.io/badge/Keras-0D1024?style=flat-square&logo=keras&logoColor=60A5FA" alt="Keras" />
<img src="https://img.shields.io/badge/scikit--learn-0D1024?style=flat-square&logo=scikitlearn&logoColor=60A5FA" alt="scikit-learn" />
<img src="https://img.shields.io/badge/NumPy-0D1024?style=flat-square&logo=numpy&logoColor=60A5FA" alt="NumPy" />
<img src="https://img.shields.io/badge/Matplotlib-0D1024?style=flat-square" alt="Matplotlib" />
<img src="https://img.shields.io/badge/React-0D1024?style=flat-square&logo=react&logoColor=60A5FA" alt="React" />
<img src="https://img.shields.io/badge/Next.js-0D1024?style=flat-square&logo=nextdotjs&logoColor=60A5FA" alt="Next.js" />
<img src="https://img.shields.io/badge/Node.js-0D1024?style=flat-square&logo=nodedotjs&logoColor=60A5FA" alt="Node.js" />
<img src="https://img.shields.io/badge/PostgreSQL-0D1024?style=flat-square&logo=postgresql&logoColor=60A5FA" alt="PostgreSQL" />
<img src="https://img.shields.io/badge/MySQL-0D1024?style=flat-square&logo=mysql&logoColor=60A5FA" alt="MySQL" />
<img src="https://img.shields.io/badge/Supabase-0D1024?style=flat-square&logo=supabase&logoColor=60A5FA" alt="Supabase" />
</p>

---

<div align="center">

<img src="https://streak-stats.demolab.com/?user=Sickwoman&hide_border=true&background=0D1024&stroke=2B3163&ring=A78BFA&fire=A78BFA&currStreakNum=60A5FA&sideNums=60A5FA&currStreakLabel=A78BFA&sideLabels=E2E8F7&dates=8B95C9" alt="GitHub contribution streak" />

<br/><br/>

<a href="https://linkedin.com/in/moksh-vatsa-a34885404"><img src="https://img.shields.io/badge/LinkedIn-0D1024?style=for-the-badge&logo=linkedin&logoColor=A78BFA" alt="LinkedIn" /></a>
<a href="mailto:vatsamoksh@gmail.com"><img src="https://img.shields.io/badge/Email-0D1024?style=for-the-badge&logo=gmail&logoColor=A78BFA" alt="Email" /></a>
<a href="https://instagram.com/notmytypebruhh"><img src="https://img.shields.io/badge/Instagram-0D1024?style=for-the-badge&logo=instagram&logoColor=A78BFA" alt="Instagram" /></a>

<br/><br/>

</div>
