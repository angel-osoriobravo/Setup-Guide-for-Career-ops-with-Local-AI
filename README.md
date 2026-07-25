# Setup-Guide-for-Career-ops-with-Local-AI
This is a personal step by step guide for how I set career ops, I was using Fedora 44 at the time and used a RTX 5070 for local AI


---

## System Setup & NVIDIA Verification

Ensure your GPU drivers and CUDA container acceleration are active before proceeding.

```bash
nvidia-smi
```

```bash
sudo dnf check-update
```

```bash
sudo dnf install -y git nodejs npm dnf-plugins-core
```

```bash
node -v
```

---

## Local AI Engine Setup (Ollama with GPU Acceleration)

Install Ollama, verify CUDA offloading on your GPU, and pull the evaluation model.

```bash
curl -fsSL [https://ollama.com/install.sh](https://ollama.com/install.sh) | sh
```

```bash
sudo systemctl enable --now ollama
```

```bash
systemctl status ollama
```

Verify Ollama detects and uses your NVIDIA GPU:

```bash
journalctl -u ollama --no-pager -n 20 | grep -i cuda
```

Pull the local evaluation model:

```bash
ollama pull mistral-nemo
```

---

## Installation

```bash
git clone [https://github.com/AngelOsorio/career-ops.git](https://github.com/AngelOsorio/career-ops.git) ~/career-ops
```

```bash
cd ~/career-ops
```

```bash
npm install
```

---

## Configuration

### Base CV Setup

Create `~/career-ops/cv.md` with structured technical sections:

```markdown
## Technical Skills
* Linux (Debian, Ubuntu, Arch)
* Proxmox VE & Unraid
* VLAN Segmentation & Juniper EX3300
* Wireshark, Splunk, TDnext

## Certifications
* CompTIA Security+
```

### Portal Scanner Configuration

Create `~/career-ops/portals.yml`:

```yaml
location_filter:
  always_allow:
    - "Your State / Region"
    - "Your Metro Area"
    - "Your City"
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
  - name: ExampleCompany1
    careers_url: [https://job-boards.greenhouse.io/examplecompany1](https://job-boards.greenhouse.io/examplecompany1)
    api: [https://boards-api.greenhouse.io/v1/boards/examplecompany1/jobs](https://boards-api.greenhouse.io/v1/boards/examplecompany1/jobs)
    enabled: true

  - name: ExampleCompany2
    careers_url: [https://job-boards.greenhouse.io/examplecompany2](https://job-boards.greenhouse.io/examplecompany2)
    api: [https://boards-api.greenhouse.io/v1/boards/examplecompany2/jobs](https://boards-api.greenhouse.io/v1/boards/examplecompany2/jobs)
    enabled: true

  - name: ExampleCompany3
    careers_url: [https://job-boards.greenhouse.io/examplecompany3](https://job-boards.greenhouse.io/examplecompany3)
    api: [https://boards-api.greenhouse.io/v1/boards/examplecompany3/jobs](https://boards-api.greenhouse.io/v1/boards/examplecompany3/jobs)
    enabled: true
```

---

## Usage

```bash
node verify-portals.mjs
```

```bash
npm run scan
```

```bash
npm run ollama:eval -- --file data/pipeline.md
```

```bash
npm run ollama:eval -- --file data/target-job.md
```

```bash
node generate-pdf.mjs cloudforce-helpdesk.html Cloudforce_Helpdesk_Technician_Resume.pdf
```
