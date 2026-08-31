# ⚡ Top Free OSINT Tools & Reconnaissance Playbook

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

An essential, beginner-to-pro guide and cheatsheet for the **best free OSINT tools (Open Source Intelligence)** used in cybersecurity, penetration testing, ethical hacking, and digital footprint mapping.

---

## 📑 Table of Contents
- [Overview](#-overview)
- [Featured Tools & Quickstarts](#-featured-tools--quickstarts)
  - [1. Maltego](#1-maltego---visual-link-analysis)
  - [2. theHarvester](#2-theharvester---emails-subdomains--ips)
  - [3. OWASP Amass](#3-owasp-amass---in-depth-attack-surface-mapping)
  - [4. Sherlock](#4-sherlock---social-media-username-hunting)
  - [5. Recon-ng](#5-recon-ng---modular-reconnaissance-framework)
  - [6. AI Recon Agents & Automation](#6-ai-recon-agents--automation)
- [💡 Pro Tips & Operational Best Practices](#-pro-tips--operational-best-practices)
- [⚖️ Legal & Ethical Disclaimer](#-legal--ethical-disclaimer)

---

## 🔍 Overview

Open Source Intelligence (**OSINT**) is the practice of collecting, analyzing, and correlating publicly available data for reconnaissance, threat intelligence, and attack surface management. This repository provides installation steps, essential CLI commands, and operational security workflows for 6 essential OSINT reconnaissance tools.

---

## 🛠 Featured Tools & Quickstarts

### 1. Maltego - Visual Link Analysis
**Purpose:** Interactive visual data-mining and graph link analysis across domains, IP blocks, individuals, organizations, and metadata.

#### 📦 Installation
- Download the community edition installer from [Maltego Official Website](https://www.maltego.com/downloads/).
- **Debian/Ubuntu/Kali:**
  ```bash
  sudo apt update && sudo apt install maltego -y

⚡ Quickstart & Usage
 * Launch GUI:
   maltego &

 * Register a free Maltego Community (CE) account.
 * Drag and drop an entity (e.g., Domain, Person, or IPv4 Address) onto the canvas, right-click, and run Standard Transforms (e.g., To DNS Name, To Email Address).
2. theHarvester - Emails, Subdomains & IPs
Purpose: Scrapes publicly exposed email addresses, names, subdomains, open ports, and banners from search engines, PGP servers, and public databases.
📦 Installation
git clone [https://github.com/laramies/theHarvester.git](https://github.com/laramies/theHarvester.git)
cd theHarvester
python3 -m pip install -r requirements/base.txt

(Or on Kali Linux: sudo apt install theharvester -y)
💻 Common Commands
 * Search target domain using Google, DuckDuckGo, and Bing:
   python3 theHarvester.py -d example.com -l 200 -b google,duckduckgo,bing

 * Run full reconnaissance and export output to HTML and XML:
   python3 theHarvester.py -d target.com -b all -f target_recon_report

3. OWASP Amass - In-Depth Attack Surface Mapping
Purpose: Network mapping, DNS enumeration, and asset discovery using open-source information gathering and active reconnaissance techniques.
📦 Installation
# Using Go
go install -v [github.com/owasp-amass/amass/v4/...@master](https://github.com/owasp-amass/amass/v4/...@master)

# Or via Snap (Linux)
sudo snap install amass

💻 Common Commands
 * Passive subdomain enumeration (non-intrusive):
   amass enum -passive -d example.com

 * Active enumeration with DNS brute-forcing and ASN tracking:
   amass enum -active -d example.com -brute -w /path/to/wordlist.txt -dir ./amass_output

 * Visualizing discovered network topology:
   amass viz -d3 -d example.com

4. Sherlock - Social Media Username Hunting
Purpose: Rapidly hunts target usernames across 400+ social media platforms and digital forums.
📦 Installation
git clone [https://github.com/sherlock-project/sherlock.git](https://github.com/sherlock-project/sherlock.git)
cd sherlock
python3 -m pip install -r requirements.txt

(Or install via pipx/pip: pip install sherlock-project)
💻 Common Commands
 * Search for a specific username across all supported platforms:
   sherlock target_username

 * Search multiple handles and output only found profiles to a folder:
   sherlock user1 user2 user3 --only-found --folderoutput ./sherlock_results/

5. Recon-ng - Modular Reconnaissance Framework
Purpose: A Metasploit-like interactive reconnaissance environment with a modular architecture for managing APIs, target databases, and automated reporting.
📦 Installation
git clone [https://github.com/lanmaster53/recon-ng.git](https://github.com/lanmaster53/recon-ng.git)
cd recon-ng
pip install -r REQUIREMENTS

💻 Common Commands
 * Launch the interactive shell:
   ./recon-ng

 * Install and configure workspace modules:
   [recon-ng][default] > workspaces create target_assessment
[recon-ng][target_assessment] > marketplace search
[recon-ng][target_assessment] > marketplace install recon/domains-hosts/brute_hosts
[recon-ng][target_assessment] > modules load recon/domains-hosts/brute_hosts
[recon-ng][target_assessment][brute_hosts] > options set SOURCE example.com
[recon-ng][target_assessment][brute_hosts] > run

6. AI Recon Agents & Automation
Purpose: Orchestrating CLI tools, parsing messy JSON/HTML output, and summarizing footprint dossiers into structured threat reports via LLM agents & automation scripts.
💡 Workflow Architecture
Target Input ──> [theHarvester / Amass / Sherlock] 
                      │ (JSON / Text Stream)
                      ▼
              [Data Normalizer] 
                      │
                      ▼
           [Local / API AI Agent] ──> Structured Risk Dossier (.md / .json)

⚡ Quick Python Pipeline Example
import subprocess
import json

def run_osint_pipeline(domain):
    print(f"[*] Running passive recon on {domain}...")
    # Execute theHarvester CLI and capture stdout
    cmd = ["theHarvester", "-d", domain, "-b", "duckduckgo", "-l", "100"]
    result = subprocess.run(cmd, capture_output=True, text=True)
    
    # Forward the findings to your custom LLM summarizer / agent pipeline
    print("[+] Recon completed. Raw data captured for analysis.")
    return result.stdout

if __name__ == "__main__":
    target = "example.com"
    run_osint_pipeline(target)

💡 Pro Tips & Operational Best Practices
 * Protect Your Source Identity (OPSEC): Always conduct OSINT research through dedicated reconnaissance machines, VPNs, or proxy chains (e.g., proxychains4) to prevent target telemetry correlation.
 * API Keys Boost Results: Tools like theHarvester, Amass, and Recon-ng perform dramatically better when supplied with free API keys (Shodan, Censys, SecurityTrails, VirusTotal, Hunter.io).
 * Automate Output Correlation: Store tool outputs in standardized JSON/CSV formats to allow easy cross-referencing and import into graph databases like Neo4j or visual platforms like Maltego.
 * Rate Limiting & False Positives: Use calibrated delays when running aggressive username or DNS brute-force queries to avoid IP throttling and transient DNS resolver failures.
⚖️ Legal & Ethical Disclaimer
> ⚠️ Warning: This repository and the tools documented herein are created strictly for educational purposes, authorized security testing, defense, and digital risk assessments. Gathering intelligence on individuals or corporate entities without explicit authorization may violate privacy regulations or terms of service. Always act responsibly and adhere to local laws.
> 
🤝 Contributing
Contributions, issues, and feature requests are welcome! Feel free to check the issues page.
⭐ If this cheat sheet helped you, please consider giving it a star!

