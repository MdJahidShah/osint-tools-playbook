# ⚡ Awesome OSINT Tools & Community Reconnaissance Playbook

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com)

A collaborative, open-source repository and cheat sheet featuring the **best free OSINT tools (Open Source Intelligence)** for reconnaissance, threat intelligence, bug bounty hunting, and attack surface discovery. 

> **Everyone is welcome to contribute!** Whether it's adding a new tool, updating CLI commands, fixing typos, or sharing OSINT investigation workflows.

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
- [🤝 How Everyone Can Contribute](#-how-everyone-can-contribute)
- [⚖️ Legal & Ethical Disclaimer](#-legal--ethical-disclaimer)

---

## 🔍 Overview

Open Source Intelligence (**OSINT**) involves gathering and correlating publicly available data to analyze security postures, track threat actors, and map digital infrastructure. This repository serves as a centralized hub containing quick-start setup instructions, copy-paste terminal commands, and actionable guidelines for the community.

---

## 🛠 Featured Tools & Quickstarts

### 1. Maltego - Visual Link Analysis
**Purpose:** Interactive visual data mining and relationship mapping across domains, IP addresses, individuals, and infrastructure.

#### 📦 Installation
- Download the installer from the [Maltego Official Website](https://www.maltego.com/downloads/).
- **Debian / Ubuntu / Kali Linux:**
  ```bash
  sudo apt update && sudo apt install maltego -y


#### ⚡ Quickstart & Usage
**Launch GUI:**
```bash
maltego &
```

* Register a free Maltego Community (CE) account.
* Add an entity (Domain, Person, IP) to the graph, right-click, and run Standard Transforms to map connections.

### 2. theHarvester - Emails, Subdomains & IPs
Purpose: Collects public email addresses, subdomains, hostnames, and employee names across multiple search engines and PGP servers.

#### 📦 Installation
```bash
git clone [https://github.com/laramies/theHarvester.git](https://github.com/laramies/theHarvester.git)
cd theHarvester
python3 -m pip install -r requirements/base.txt
```

(On Kali Linux: sudo apt install theharvester -y)

#### 💻 Common Commands
**Query multiple search engines for subdomains and emails:**
```bash
python3 theHarvester.py -d example.com -l 200 -b google,duckduckgo,bing
```


**Run a full source scan and save results to HTML/XML:**
```bash
python3 theHarvester.py -d example.com -b all -f osint_report
```

### 3. OWASP Amass - In-Depth Attack Surface Mapping
**Purpose:** Advanced DNS enumeration, network mapping, and infrastructure discovery using active and passive data sources.

#### 📦 Installation

#### Using Go
```bash
go install -v [github.com/owasp-amass/amass/v4/...@master](https://github.com/owasp-amass/amass/v4/...@master)

# Or via Snap (Linux)
sudo snap install amass
```

#### 💻 Common Commands
Non-intrusive passive subdomain enumeration:
```bash
amass enum -passive -d example.com
```

Active reconnaissance with DNS brute-forcing:
```bash
amass enum -active -d example.com -brute -w /path/to/wordlist.txt -dir ./amass_output
```

### 4. Sherlock - Social Media Username Hunting
**Purpose:** Scans over 400+ social networks and digital forums to locate accounts registered under a specific username.
#### 📦 Installation
```bash
git clone [https://github.com/sherlock-project/sherlock.git](https://github.com/sherlock-project/sherlock.git)
cd sherlock
python3 -m pip install -r requirements.txt
```
Or via pip:
```bash
pip install sherlock-project
```

#### 💻 Common Commands
**Search for a specific handle:**
```bash
sherlock username_to_search
```

Search multiple accounts and output only active links to a folder:
```bash
sherlock user1 user2 --only-found --folderoutput ./sherlock_results/
```

### 5. Recon-ng - Modular Reconnaissance Framework
**Purpose:** A full-featured, Metasploit-style CLI framework for automated intelligence gathering with database and API integration.

#### 📦 Installation
```bash
git clone [https://github.com/lanmaster53/recon-ng.git](https://github.com/lanmaster53/recon-ng.git)
cd recon-ng
pip install -r REQUIREMENTS
```

#### 💻 Common Commands
**Launch the interactive shell:**
```bash
./recon-ng
```

**Initialize a workspace and run modules:**
* [recon-ng][default]** > workspaces create target_assessment
* **[recon-ng][target_assessment]** > marketplace install recon/domains-hosts/brute_hosts
* **[recon-ng][target_assessment]** > modules load recon/domains-hosts/brute_hosts
* **[recon-ng][target_assessment][brute_hosts]** > options set SOURCE example.com
* **[recon-ng][target_assessment][brute_hosts]** > run


### 6. AI Recon Agents & Automation
**Purpose:** Running automated CLI scripts and passing raw reconnaissance data to LLMs for summarizing, noise reduction, and threat dossier formatting.

#### ⚡ Sample Automation Pipeline
```bash
import subprocess

def run_osint_pipeline(domain: str):
    print(f"[*] Running passive recon on {domain}...")
    cmd = ["theHarvester", "-d", domain, "-b", "duckduckgo", "-l", "100"]
    result = subprocess.run(cmd, capture_output=True, text=True)
    
    print("[+] Reconnaissance completed. Forwarding to analysis agent.")
    return result.stdout

if __name__ == "__main__":
    run_osint_pipeline("example.com")
```

## 💡 Pro Tips & Operational Best Practices
* **Maintain OPSEC:** Use isolated testing environments, VPNs, or proxy chains (proxychains4) to avoid exposing your personal IP during OSINT scans.
* **Integrate Free API Keys:** Add free API keys (Shodan, Censys, VirusTotal, Hunter.io) to tools like theHarvester and Amass to unlock far deeper intelligence.
* **Export to Standard Formats:** Save outputs in JSON or CSV to make data aggregation and cross-referencing across different tools seamless.
  
#### 🤝 How Everyone Can Contribute
We welcome contributions from everyone—from beginners to seasoned security researchers!
Fork the Repository

**Create a Feature Branch:**
```bash
git checkout -b feature/add-new-osint-tool
```

**Commit Your Changes:**
```bash
git commit -m "Add SpiderFoot installation and quickstart guide"
```

**Push to Your Branch:**
```bash
git push origin feature/add-new-osint-tool
```

Open a Pull Request describing what you added or improved.

### Ways to Contribute:
* 📌 Add new open-source OSINT tools or scripts.
* 📝 Improve documentation, formatting, or command references.
* 🐛 Fix broken links, typos, or outdated installation commands.
* 💡 Share useful dork lists, cheat sheets, or automation workflows.
* 
## ⚖️ Legal & Ethical Disclaimer
**⚠️ Notice:** This repository is intended solely for educational purposes, authorized security testing, defense, and research. Always ensure you have appropriate authorization before assessing domains or infrastructure you do not own.

## 🌟 Show Your Support
If you found this playbook useful, give it a ⭐ Star and share it with your network!

