# Setup-Guide-for-Career-ops-with-Local-AI
This is a personal step by step guide for how I set career ops as a fun way, I was using Fedora 44 at the time and used a RTX 5070

career-ops Setup Guide (Fedora)

Complete installation and configuration guide for running career-ops on Fedora Linux.
Prerequisites

sudo dnf check-update

sudo dnf install -y git nodejs npm dnf-plugins-core

node -v
Local AI Engine Setup

curl -fsSL [https://ollama.com/install.sh](https://ollama.com/install.sh) | sh

sudo systemctl enable --now ollama

ollama pull mistral-nemo
Installation

git clone [https://github.com/AngelOsorio/career-ops.git](https://github.com/AngelOsorio/career-ops.git) ~/career-ops

cd ~/career-ops

npm install
Configuration
Base CV Setup

Create ~/career-ops/cv.md with structured technical sections:
Markdown

## Technical Skills
* Linux (Debian, Ubuntu, Arch)
* Proxmox VE & Unraid
* VLAN Segmentation & Juniper EX3300
* Wireshark, Splunk, TDnext

## Certifications
* CompTIA Security+

Portal Scanner Configuration

Create ~/career-ops/portals.yml:
YAML

location_filter:
  always_allow:
    - "Maryland"
    - "MD"
    - "Virginia"
    - "VA"
    - "District of Columbia"
    - "Washington DC"
    - "DC"
    - "Chantilly"
    - "Ashburn"
  allow:
    - "Remote"
    - "United States"
    - "US"

title_filter:
  positive:
    - "Network"
    - "Systems"
    - "NOC"
    - "SOC"
    - "Infrastructure"
    - "Data Center"
    - "IT Specialist"
    - "Support"
    - "Technician"
  negative:
    - "Senior"
    - "Sr."
    - "Lead"
    - "Manager"
    - "Director"

tracked_companies:

Usage

node verify-portals.mjs

npm run scan

npm run ollama:eval -- --file data/pipeline.md

npm run ollama:eval -- --file data/target-job.md

node generate-pdf.mjs cloudforce-helpdesk.html Cloudforce_Helpdesk_Technician_Resume.pdf
