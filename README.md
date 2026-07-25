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
  - name: CoreWeave
    careers_url: [https://job-boards.greenhouse.io/coreweave](https://job-boards.greenhouse.io/coreweave)
    api: [https://boards-api.greenhouse.io/v1/boards/coreweave/jobs](https://boards-api.greenhouse.io/v1/boards/coreweave/jobs)
    enabled: true

  - name: Cloudflare
    careers_url: [https://job-boards.greenhouse.io/cloudflare](https://job-boards.greenhouse.io/cloudflare)
    api: [https://boards-api.greenhouse.io/v1/boards/cloudflare/jobs](https://boards-api.greenhouse.io/v1/boards/cloudflare/jobs)
    enabled: true

  - name: Datadog
    careers_url: [https://job-boards.greenhouse.io/datadog](https://job-boards.greenhouse.io/datadog)
    api: [https://boards-api.greenhouse.io/v1/boards/datadog/jobs](https://boards-api.greenhouse.io/v1/boards/datadog/jobs)
    enabled: true

  - name: Appian
    careers_url: [https://job-boards.greenhouse.io/appian](https://job-boards.greenhouse.io/appian)
    api: [https://boards-api.greenhouse.io/v1/boards/appian/jobs](https://boards-api.greenhouse.io/v1/boards/appian/jobs)
    enabled: true

  - name: CoStar
    careers_url: [https://job-boards.greenhouse.io/costar](https://job-boards.greenhouse.io/costar)
    api: [https://boards-api.greenhouse.io/v1/boards/costar/jobs](https://boards-api.greenhouse.io/v1/boards/costar/jobs)
    enabled: true

  - name: Tailscale
    careers_url: [https://job-boards.greenhouse.io/tailscale](https://job-boards.greenhouse.io/tailscale)
    api: [https://boards-api.greenhouse.io/v1/boards/tailscale/jobs](https://boards-api.greenhouse.io/v1/boards/tailscale/jobs)
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
