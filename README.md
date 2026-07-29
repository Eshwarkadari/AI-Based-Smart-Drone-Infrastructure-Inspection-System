# 🛰️ Aero Vaani — AI-Based Smart Drone Infrastructure Inspection System

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-27338e?style=for-the-badge&logo=OpenCV&logoColor=white)
![Raspberry Pi](https://img.shields.io/badge/Raspberry_Pi-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white)
![MIT License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Hackathon Winner](https://img.shields.io/badge/🏆_Winner-Hacksavvy--26-FFD700?style=for-the-badge)

**🏆 Winner — Hacksavvy-26 | 24-Hour National Hackathon | MGIT**

*Built by Team Aero Vaani — CMR College of Engineering & Technology (CMRCET), Hyderabad*

[🚀 Run Locally](#-installation) · [📖 Architecture](#-architecture) · [🧪 Tests](#-running-tests) · [🔮 Roadmap](#-future-improvements)

</div>

---

## 📌 What Is Aero Vaani?

An **autonomous drone-based inspection system** that flies to critical infrastructure (transmission towers, electric poles, bridges), captures live imagery, detects structural cracks using computer vision, tags findings with GPS coordinates, classifies damage severity into three action zones, and automatically generates and emails a professional PDF inspection report — **without a human ever having to climb the structure.**

---

## 📌 Problem Statement

Manual inspection of infrastructure is:

| Problem | Impact |
|---------|--------|
| ⏱️ Time-consuming | Each structure requires a physical visit |
| 💸 Expensive | Specialized equipment + trained personnel |
| ⚠️ Risky | Inspectors work at height / near live equipment |
| 📋 Inconsistent | Assessments vary; rarely GPS-logged |

**Aero Vaani** automates this entire workflow — from flight to inbox.

---

## ✨ Features

- 📷 **Live image capture** from Raspberry Pi Camera Module during flight
- 📍 **GPS & flight telemetry** from Pixhawk flight controller via MAVLink
- 🧠 **AI/CV crack detection** — OpenCV edge + contour pipeline optimized for Raspberry Pi
- 🟢🟡🔴 **Three-tier severity classification**:

  | Zone | Label | Action Window |
  |------|-------|--------------|
  | 🟢 Green | Minor Damage | Inspect within 7 days |
  | 🟡 Yellow | Moderate Damage | Maintenance within 3 days |
  | 🔴 Red | Critical Damage | Immediate action within 24 hours |

- 📊 **Live web dashboard** — real-time image, GPS, telemetry, classification
- 📄 **Auto PDF report** — GPS-tagged, severity-classified, with annotated image
- 📧 **Automated email delivery** of report to registered recipients
- 🧪 **Simulation mode** — full pipeline runs on a laptop with zero hardware

---

## 🏗️ Architecture

```
                    ┌────────────────────┐
                    │   Pixhawk Flight   │
                    │    Controller      │──── GPS + Telemetry (MAVLink)
                    └─────────┬──────────┘
                              │
   ┌──────────────────┐      │      ┌──────────────────────┐
   │  Raspberry Pi    │◄─────┘      │  Raspberry Pi Camera  │
   │ (onboard compute)│◄────────────│      Module           │
   └─────────┬────────┘             └──────────────────────┘
             │  captured frame + telemetry
             ▼
   ┌──────────────────────────┐
   │  Computer Vision Engine  │   OpenCV: Gaussian blur → Canny
   │  vision/crack_detector   │   → morphological filter → contours
   └─────────────┬────────────┘
                 ▼
   ┌──────────────────────────┐
   │   Severity Classifier    │   Green / Yellow / Red zone logic
   └─────────────┬────────────┘
                 ▼
   ┌──────────────────────────┐        ┌─────────────────────────┐
   │   PDF Report Generator   │───────►│   Email Automation      │
   └─────────────┬────────────┘        └─────────────────────────┘
                 ▼
   ┌──────────────────────────┐
   │   Flask Web Dashboard    │   Live view of every inspection
   └──────────────────────────┘
```

---

## 📁 Project Structure

```
AI-Based-Smart-Drone-Infrastructure-Inspection-System/
├── run.py                        # 🚀 App entrypoint
├── requirements.txt              # Python dependencies
├── .env.example                  # Environment template (no secrets)
├── app/                          # Flask application
│   ├── __init__.py               #   App factory
│   ├── config.py                 #   Environment-based config
│   ├── routes.py                 #   Inspection pipeline API
│   ├── static/css/style.css      #   Dashboard styles
│   └── templates/                #   Jinja2 HTML templates
├── drone/                        # 🚁 Hardware interfaces
│   ├── camera.py                 #   Picamera2 + simulation fallback
│   └── telemetry.py              #   MAVLink/Pixhawk + simulation fallback
├── vision/                       # 🧠 Computer vision
│   ├── crack_detector.py         #   OpenCV crack detection
│   └── severity_classifier.py   #   Green/Yellow/Red classifier
├── reports/                      # 📄 PDF generation (ReportLab)
├── notifications/                # 📧 Email automation (SMTP)
├── tests/                        # 🧪 pytest unit tests
├── data/
│   ├── sample_images/            # Sample inspection images
│   └── inspection_logs/          # Generated PDFs & captures
└── docs/
    ├── architecture.md
    └── screenshots/              # ← Hackathon photos go here
```

---

## 🚀 Installation

### Quick Start (Simulation Mode — no hardware needed)

```bash
# 1. Clone
git clone https://github.com/Eshwarkadari/AI-Based-Smart-Drone-Infrastructure-Inspection-System.git
cd AI-Based-Smart-Drone-Infrastructure-Inspection-System

# 2. Virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install
pip install -r requirements.txt

# 4. Configure
cp .env.example .env

# 5. Run
python run.py
```

Open **http://localhost:5000** and click **"Run Inspection"** 🚁

> `SIMULATION_MODE=True` by default — synthetic frames + GPS generated automatically. No drone required!

---

## ▶️ Run in GitHub Codespaces (Zero Install!)

1. Click green **"Code"** → **"Codespaces"** → **"Create codespace on main"**
2. Wait ~1 minute for setup
3. In terminal: `pip install -r requirements.txt && python run.py`
4. Click **"Open in Browser"** → Dashboard opens! ✅

---

## 🧪 Running Tests

```bash
pytest tests/ -v
```

---

## 📸 Screenshots

> *(Hackathon photos coming soon — see [docs/screenshots/](docs/screenshots/))*

| Dashboard | Inspection Result | PDF Report |
|-----------|-------------------|------------|
| *Coming soon* | *Coming soon* | *Coming soon* |

---

## 🧗 Engineering Challenges Solved in 24 Hours

- MAVLink communication reliability between Raspberry Pi and Pixhawk
- Raspberry Pi camera memory constraints during continuous capture
- GPS synchronization with image capture timing
- Real-time telemetry integration into the Flask dashboard
- OpenCV pipeline optimization for near-real-time crack detection on Pi
- Reducing false positives using rotation-aware bounding boxes (minAreaRect)
- End-to-end PDF generation + email automation pipeline

---

## 🔮 Future Improvements

- [ ] Replace classical CV with deep-learning segmentation (U-Net / YOLO)
- [ ] Autonomous flight path planning around structures
- [ ] Historical inspection dashboard with trend analysis
- [ ] Multi-drone fleet support
- [ ] Offline-first mobile companion app for field engineers
- [ ] GIS platform integration for asset-level tracking

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Onboard compute | Raspberry Pi 3 Model B+ |
| Camera | Raspberry Pi Camera + Picamera2 |
| Flight controller | Pixhawk (GPS + MAVLink) |
| Backend | Python 3 + Flask |
| Computer vision | OpenCV |
| Telemetry | MAVLink via pymavlink |
| PDF reports | ReportLab |
| Email | smtplib (SMTP) |
| Frontend | HTML + CSS + JavaScript |
| Testing | pytest |

---

## 👥 Team Aero Vaani

**Kadari Eshwar** — [GitHub](https://github.com/Eshwarkadari) | [LinkedIn](https://www.linkedin.com/in/eshwar-kadari-134aa4278)

*CMR College of Engineering & Technology (CMRCET), Hyderabad*

🏆 **Winner — Hacksavvy-26 | 24-Hour National Hackathon | MGIT**

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
