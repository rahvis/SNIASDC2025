# Design Specification and AI‑Driven Digital Twin Architecture for Storage Devices

> **SNIA Developer Conference (SDC) — Session: Design Specification and AI‑Driven Digital Twin Architecture for Storage Devices**  
> Session page: https://www.snia.org/sniadeveloper/session/19345

This repository accompanies the SNIA SDC talk on using open standards (DMTF **Redfish** and SNIA **Swordfish**) together with modern AI techniques to generate faithful **digital twins** of storage and datacenter devices. The goal is to help teams design, validate, and demo against *standards‑compliant* virtual hardware—without waiting for scarce, expensive prototypes.

**Code:** https://github.com/rahvis/DMTF-Redfish-Digital-Twin

---

## Table of contents
- [Why this matters](#why-this-matters)
- [What’s in this repo](#whats-in-this-repo)
- [Architecture at a glance](#architecture-at-a-glance)
- [Quickstart](#quickstart)
- [Configuration](#configuration)
- [Demos & scenarios](#demos--scenarios)
- [Interop & ecosystem](#interop--ecosystem)
- [Slides / video](#slides--video)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Citation](#citation)
- [License](#license)

---

## Why this matters

Hardware programs are constrained by limited proto units, tight schedules, and high costs. This project demonstrates a **software‑first** approach: automatically generate Redfish/Swordfish‑compliant device models, validate them against schemas and policy rules, and emit a Redfish‑style folder tree that existing tools can consume.

---

## What’s in this repo

- **Specification‑driven generation** using Redfish/Swordfish schemas, profiles, and mockups  
- **AI‑assisted synthesis** to produce realistic resource graphs for common storage topologies  
- **Validation hooks**: required fields, types, value constraints, and JSON Schema checks  
- **Standards‑compliant output**: Redfish directory layout with `index.json` resources and collections  
- **Scenario presets** for enterprise storage, HPC, modular infrastructure, edge, cloud‑native, and AI/ML

> The reference implementation and sample scripts live in the code repository linked above:  
> **https://github.com/rahvis/DMTF-Redfish-Digital-Twin**

---

## Architecture at a glance

```
Redfish/Swordfish Schemas & Mockups
              │
              ▼
       Prompt / Model Builder ──► examples + constraints
              │
              ▼
        Simulation Engine ──► AI generation (guardrailed)
              │
              ▼
       Response Validator ──► policy + JSON Schema checks
              │
              ▼
     Recording Generator ──► Redfish-compliant output tree
```

- **Inputs**: official schemas, profiles, and example mockups  
- **Core**: generation + validation loop with explicit constraints  
- **Outputs**: Redfish/Swordfish‑compliant recordings that tools can read

---

## Quickstart

> These are typical steps. If this repo includes a `requirements.txt` or `pyproject.toml`, use that instead. Adjust paths/commands to your environment.

### Clone
```bash
git clone https://github.com/rahvis/DMTF-Redfish-Digital-Twin.git
cd DMTF-Redfish-Digital-Twin
```

### Create & activate a virtual environment
```bash
python -m venv .venv
# Linux/macOS:
source .venv/bin/activate
# Windows (PowerShell):
# .\.venv\Scripts\Activate.ps1
```

### Install dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt  # if present
```

### Run a demo (example)
```bash
# Replace with the actual entry point in the repo if different
python demo.py
```

### Where outputs go
Generated recordings typically land under an `output/` directory (or as documented in the code repo), e.g.:
```
output/recordings/<DeviceType_ResourceType_YYYYMMDD_HHMMSS>/redfish/v1/...
```

### Optional: Docker
If a `Dockerfile` is provided in the code repo, a common pattern is:
```bash
docker build -t digital-twin-demo:latest .
docker run --rm -v $(pwd)/output:/app/output digital-twin-demo:latest
```

---

## Configuration

Typical configuration values you may see in the implementation:
- **Schema versions / locations**: where Redfish/Swordfish schemas or mockups are stored
- **Validation settings**: toggle strict JSON Schema checks or allow warnings
- **Scenario presets**: choose a topology (enterprise storage, AI/ML, edge, etc.)
- **Model/provider settings** (if AI is used): API keys, endpoints, and model names

> Refer to the code repository for the exact configuration file(s) and environment variables.

---

## Demos & scenarios

- Predefined scenarios (e.g., `enterprise_storage`, `ai_ml_ready`, `edge_computing`) can be used to seed realistic device graphs.  
- Extend with your own prompts or templates to represent vendor‑specific features.  
- Tighten/relax validation via policy and JSON Schema rules.

---

## Interop & ecosystem

Designed to work with the Redfish tooling ecosystem (validators, mockup servers, interface emulators) and SNIA Swordfish extensions. You can feed the generated recordings into CI flows, client SDKs, or demo environments to validate management operations before hardware is available.

---

## Slides / video

- **Session page:** https://www.snia.org/sniadeveloper/session/19345  
- (Recording/link will be added here when available.)

---

## FAQ

**Q: Do I need internet access to run the demos?**  
A: Only if the implementation uses an external AI provider or fetches schemas from the web. Local‑only runs are possible when everything is vendored.

**Q: Will the output be accepted by Redfish clients?**  
A: The goal is standards compliance. Use the provided validation steps (and, where relevant, official validators) to ensure conformance.

**Q: Can I model non‑storage devices?**  
A: Yes, any device with a Redfish‑style model can be represented; Swordfish extends Redfish for storage semantics.

---

## Contributing

Issues and PRs are welcome! For major changes, please open an issue first to discuss the direction and design.

---

## Citation

If you reference the talk or this repository, please cite:

```
Design Specification and AI‑Driven Digital Twin Architecture for Storage Devices.
SNIA Developer Conference (SDC). 
Session page: https://www.snia.org/sniadeveloper/session/19345
Code: https://github.com/rahvis/DMTF-Redfish-Digital-Twin
```

---

## License

See `LICENSE` for details. If no license is present, please open an issue to clarify terms.
