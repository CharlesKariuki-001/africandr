# 🛡️ AfricaNDR — AI-Powered Network Detection & Response

> Built for African infrastructure. Powered by AI. Deployable anywhere.

[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-blue?style=flat&logo=python)](https://python.org)
[![Zeek](https://img.shields.io/badge/Zeek-NDR-orange?style=flat)](https://zeek.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat)](LICENSE)
[![Built in Public](https://img.shields.io/badge/Built-In%20Public-blueviolet?style=flat)](https://ke.linkedin.com/in/charles-mburu-838965382)
[![Part of Vigilant AI](https://img.shields.io/badge/Part%20of-Vigilant%20AI-red?style=flat)](https://github.com/CharlesKariuki-001/VigilantAI)

---

## What Is AfricaNDR?

AfricaNDR is an open-source **Network Detection & Response (NDR) system** built specifically for African network environments — with a focus on mobile money infrastructure, USSD-based transactions, and fintech API security.

It captures live network traffic, extracts behavioral features, runs ML-based anomaly detection, and generates actionable alerts — all on minimal hardware.

This is not a Western NDR tool adapted for Africa. This is built from scratch, for African threat models.

---

## Why This Exists

African mobile money systems process billions of dollars in transactions with almost zero dedicated network-layer security. SACCOs, fintechs, mobile money agents, and microfinance institutions have no visibility into what is happening on their own networks.

The threats are real and they are happening right now:

- SIM swap attacks that bypass app-layer controls entirely
- Mobile money API abuse and automated credential stuffing
- USSD session anomalies that signal account takeover
- Agent network compromise and insider threat patterns
- Lateral movement inside fintech infrastructure

AfricaNDR detects these at the **network layer** — before they complete.

---

## Architecture
[Network Traffic]

│

▼

┌─────────────┐     ┌──────────────────────┐

│    Zeek     │────▶│  Structured Log Data  │

│  (Sensor)   │     │  conn / dns / http    │

└─────────────┘     └──────────┬───────────┘

│

▼

┌──────────────────────┐

│  Feature Extraction   │

│  (flow-level + graph) │

└──────────┬───────────┘

│

▼

┌──────────────────────┐     ┌─────────────────┐

│     ML Engine         │────▶│  Alert System   │

│  Anomaly + Classifier │     │  + Dashboard    │

└──────────────────────┘     └─────────────────┘

│

▼

┌──────────────────────┐

│  Vigilant AI Bridge   │

│  Network + Fraud Score│

└──────────────────────┘

---

## Project Structure
africandr/

├── src/

│   ├── capture/           # Zeek log parsing + PCAP reading

│   ├── detection/         # Rules engine + anomaly detector

│   ├── ml/                # Feature extraction + ML models

│   ├── dashboard/         # Streamlit alert dashboard

│   └── utils/             # Config, logger, helpers

│

├── zeek_scripts/          # Custom Zeek detection scripts

│   ├── port_scan_detect.zeek

│   ├── dns_tunnel_detect.zeek

│   ├── mobile_money_monitor.zeek

│   └── c2_beacon_detect.zeek

│

├── notebooks/             # Learning + analysis notebooks

│   ├── 01_zeek_log_analysis.ipynb

│   ├── 02_feature_engineering.ipynb

│   ├── 03_anomaly_detection_model.ipynb

│   └── 04_african_fintech_traffic_analysis.ipynb

│

├── datasets/              # Download instructions (not included)

├── reports/templates/     # Security assessment report templates

├── docs/                  # Setup guides + threat model docs

├── tests/

├── requirements.txt

└── README.md

---

## Threat Models Covered

**General network threats:**
- Port scanning and network reconnaissance
- C2 (Command & Control) beaconing
- DNS tunneling
- Lateral movement
- Data exfiltration patterns

**African fintech specific:**
- SIM swap network-layer indicators
- Mobile money API abuse patterns
- USSD session anomalies
- Agent network compromise behavior
- Unusual transaction velocity at the network layer

Full threat model documentation in `docs/threat_models/`.

---

## Build Progress

| Module | Status | Description |
|--------|--------|-------------|
| Zeek Log Parser | ✅ Done | Parse conn / dns / http / ssl logs |
| PCAP Reader | ✅ Done | Read and summarize .pcap files |
| Feature Extractor | 🔄 In Progress | Flow-level feature engineering |
| Anomaly Detector | 🔄 In Progress | Isolation Forest on flow data |
| Rules Engine | 📋 Planned | Signature-based detection |
| ML Classifier | 📋 Planned | Trained on CIC-IDS2017 dataset |
| Alert Dashboard | 📋 Planned | Streamlit live visualization |
| Vigilant AI Bridge | 📋 Planned | Combined network + fraud scoring |

---

## Quick Start

**Requirements:** Python 3.10+, Linux (Ubuntu 22.04 recommended), Zeek 6.x for live capture.

```bash
# Clone
git clone https://github.com/CharlesKariuki-001/africandr.git
cd africandr

# Setup
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env

# Run on a PCAP file
python src/capture/pcap_reader.py --file datasets/sample/traffic.pcap

# Run on Zeek logs
python src/capture/zeek_parser.py --log-dir /path/to/zeek/logs/ --summary

# Launch dashboard
streamlit run src/dashboard/app.py
```

---

## Datasets

| Dataset | Source | Purpose |
|---------|--------|---------|
| CIC-IDS2017 | University of New Brunswick | ML model training |
| CIC-IDS2018 | University of New Brunswick | Model validation |
| UNSW-NB15 | UNSW Canberra | Anomaly detection testing |
| Self-generated | Home lab (GNS3) | African traffic simulation |

Datasets are not included due to size. See `datasets/README.md` for download links.

---

## Connection to Vigilant AI

AfricaNDR feeds directly into [Vigilant AI](https://github.com/CharlesKariuki-001/VigilantAI), my AI-powered fraud detection system for African mobile money.

Most fraud detection systems operate at the **transaction layer** only — they see the transaction after it happens. AfricaNDR adds the **network layer** — it sees the attack as it is being set up. Combining both layers produces a risk score that is significantly harder to evade.
AfricaNDR signal  +  Vigilant AI signal  =  Combined Risk Score

(Network anomaly)    (Transaction fraud)     (Harder to evade)

---

## Roadmap

- [ ] Month 1–3: Zeek parser, PCAP reader, home lab setup, first notebooks
- [ ] Month 4–6: Feature engineering, Isolation Forest anomaly detector
- [ ] Month 7–9: Dashboard, alert system, African fintech traffic module
- [ ] Month 10–12: Vigilant AI bridge, real-world lab deployment
- [ ] Month 13–15: First SACCO or fintech deployment
- [ ] Month 16–18: Productize, consulting engagements, open pilot program

---

## Built In Public

This is being built week by week as part of an 18-month AI Security engineering grind. Progress is documented publicly — real builds, real failures, real learning.

- LinkedIn: [Charles Mburu](https://ke.linkedin.com/in/charles-mburu-838965382)

One post per week. No fake highlights.

---

## License

MIT — open for learning, building, and adapting.

---

## Author

**Charles Kariuki (Charles Mburu)**  
Final-Year CS Student · Aspiring AI Security Engineer · Founder, Vigilant AI  
Nairobi, Kenya 🇰🇪
