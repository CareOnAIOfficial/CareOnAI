<div align="center">
<img src="https://img.shields.io/badge/AI-Careon-1B4F8A?style=for-the-badge&logo=heart&logoColor=white" alt="AI Careon"/>
# 🛏️ AI Careon
### Intelligent Bed Sore Prevention System
 
**Real-time · AI-powered · Autonomous pressure relief for immobile patients**
 
<br/>
<<<<<<< HEAD

=======
[![ESP8266](https://img.shields.io/badge/ESP8266-NodeMCU-blue?style=flat-square&logo=arduino)](https://www.arduino.cc/)
[![TensorFlow Lite](https://img.shields.io/badge/TensorFlow-Lite-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)](https://www.tensorflow.org/lite)
[![Firebase](https://img.shields.io/badge/Firebase-Realtime_DB-FFCA28?style=flat-square&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Blynk](https://img.shields.io/badge/Blynk-IoT_App-00E5FF?style=flat-square)](https://blynk.io/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
 
<br/>
>>>>>>> 5cd37dee896bda6fb84e9fd151dd337b62ddc980
> *Bed sores affect **2.5 million** patients per year and cost **$11 billion** annually in the US alone.  
> AI Careon prevents them — automatically, intelligently, and affordably.*
 
</div>
---
 
## 📋 Table of Contents
 
- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [How It Works](#-how-it-works)
- [System Architecture](#-system-architecture)
- [Sensors](#-sensors)
- [Actuation Systems](#-actuation-systems)
- [AI & Algorithms](#-ai--algorithms)
- [Cloud & App](#-cloud--app)
- [Hardware Build](#-hardware-build)
- [Software Setup](#-software-setup)
- [Results & Impact](#-results--impact)
- [Team](#-team)
---
 
## 🚨 The Problem
 
**Pressure ulcers (bed sores)** are localized injuries to the skin and underlying tissue caused by sustained pressure cutting off blood supply. They affect patients who cannot reposition themselves — ICU patients, spinal cord injuries, stroke survivors, and the elderly.
 
| Statistic | Data |
|-----------|------|
| Global hospital prevalence | 10–18% of all inpatients |
| ICU patients affected | Up to 41% |
| Annual cases (USA) | 2.5 million per year |
| Annual deaths (USA) | ~60,000 |
| Cost per severe case | $20,000 – $150,000+ |
| Total annual cost (USA) | $11 billion |
 
### Why existing solutions fail
 
Traditional prevention relies entirely on nurses manually repositioning patients every 2 hours. This fails regularly due to:
- Night shifts and understaffing
- No real-time monitoring of actual tissue risk
- No patient-specific intelligence
- No automatic physical intervention
---
 
## 💡 Our Solution
 
**AI Careon** is a smart mattress-integrated system that:
 
1. **Continuously monitors** pressure, temperature, humidity, motion, heart rate, and SpO2
2. **Analyzes risk** in real time using a multi-layer AI system
3. **Automatically acts** — inflates air bladders, triggers vibration, adjusts bed position
4. **Alerts caregivers** via mobile app and audible/visual indicators
> ✅ Prevention cost: **~$140 in hardware**  
> 🏥 Commercial equivalent: **$2,000 – $20,000**
 
---
 
## ⚙️ How It Works
 
```
┌─────────────────────────────────────────────────────────────────┐
│                        AI CAREON PIPELINE                       │
├──────────────┬──────────────────┬───────────────┬──────────────┤
│   SENSING    │    PROCESSING    │   ACTUATION   │    CLOUD     │
│              │                  │               │              │
│ FSR ───────► │                  │ ► Air Pump    │ ► Firebase   │
│ DHT22 ─────► │   ESP8266        │ ► Vibration   │ ► Blynk App  │
│ MPU-6050 ──► │   + AI Model     │ ► Bed Tilt    │ ► Push Alert │
│ MAX30102 ──► │                  │ ► LED + Buzzer│              │
│ HX711 ─────► │   Risk Score     │               │              │
│ Moisture ──► │   0 ──────► 100  │               │              │
└──────────────┴──────────────────┴───────────────┴──────────────┘
```
 
### Decision Flow
 
```
Sensor reading
      │
      ▼
Moving Average Filter  ──►  Clean data
      │
      ▼
Time Analysis  ──►  How long has pressure been applied?
      │
      ▼
Rule-Based Engine  ──►  Immediate threshold violations?
      │
      ▼
Decision Tree  ──►  Multi-factor composite score (0–100)
      │
      ▼
TinyML Model  ──►  Learned patterns from real patient data
      │
      ▼
Risk Score ──► < 40: Safe  │  40–60: Caution  │  60–80: Danger  │  > 80: Critical
                    │              │                  │                  │
                 Log only     Vibration +       Air pump +        Raise bed +
                              App alert         App alert         Air pump +
                                                                  CRITICAL alert
```
 
---
 
## 🏗️ System Architecture
 
```
                    ┌─────────────────────────────────┐
                    │         AI CAREON SYSTEM         │
                    └─────────────────────────────────┘
                                    │
          ┌─────────────────────────┼─────────────────────────┐
          │                         │                         │
   ┌──────▼──────┐          ┌───────▼──────┐         ┌───────▼──────┐
   │   LAYER 1   │          │   LAYER 2    │         │   LAYER 3    │
   │  SENSING    │          │  PROCESSING  │         │  ACTUATION   │
   │             │          │              │         │              │
   │ 9 Sensors   │──data──► │  ESP8266     │──cmds──►│ Air Bladders │
   │             │          │  + TinyML    │         │ Vibration    │
   └─────────────┘          │  + Rules     │         │ Linear Act.  │
                            │  + Firebase  │         │ LED + Buzzer │
                            └──────┬───────┘         └─────────────┘
                                   │
                            ┌──────▼───────┐
                            │    CLOUD     │
                            │  Firebase    │
                            │  Blynk App  │
                            └─────────────┘
```
 
---
 
## 📡 Sensors
 
| Sensor | Model | Placement | Purpose |
|--------|-------|-----------|---------|
| **Pressure (FSR)** | FSR 402 | Back · Hip · Heel | Detect dangerous contact pressure |
| **Temp & Humidity** | DHT22 | Inside mattress | Monitor skin moisture environment |
| **Motion / Posture** | MPU-6050 GY-521 | Mattress center | Detect immobility & posture |
| **Pressure Matrix** | Velostat sheet | Full body surface | Complete pressure map |
| **Weight** | Load Cell + HX711 | Under bed legs | Precise weight & shift detection |
| **Heart Rate** | MAX30102 | Fingertip | Circulation monitoring |
| **SpO2** | MAX30102 | Fingertip | Blood oxygen saturation |
| **Surface Moisture** | Capacitive sensor | Mattress surface | Detect wetness / incontinence |
| **Vibration / Energy** | Piezo disc 27mm | Under mattress | Motion sensing + energy harvesting |
 
### Mattress Layer Stack
 
```
┌─────────────────────────────────────────────────────┐  Layer 1
│           Breathable medical-grade cover             │  ~2 cm
├─────────────────────────────────────────────────────┤  Layer 2
│  ● ● ● ● ● ●  Surface moisture sensor mesh  ● ● ●  │  ~3 mm
├────────────┬───────────────────────────┬────────────┤  Layer 3
│ [FSR]      │      [MPU-6050]  [DHT22]  │      [FSR] │  ~5 mm
├────────────┼───────────────────────────┼────────────┤  Layer 4
│ (air cell) │     (air cell — sacrum)   │ (air cell) │  ~4 cm
│            │                           │            │
├────────────┴───────────────────────────┴────────────┤  Layer 5
│  · · · · ·  Velostat pressure matrix  · · · · · ·  │  ~4 mm
├─────────────────────────────────────────────────────┤  Layer 6
│   M    M    M    M    M    M   Vibration + foam     │  ~8 cm
└─────────────────────────────────────────────────────┘
```
> M = Coin vibration motor
 
---
 
## 🦾 Actuation Systems
 
### 1. Air Pressure System
Inflatable bladders under high-risk zones automatically cycle to redistribute pressure.
 
```
ESP8266 ──► Relay ──► 12V Air Pump ──► Air Bladder (inflate 30s)
                  └──► Solenoid Valve ──► Release (deflate 30s)
```
 
### 2. Vibration Motors
6× coin motors create gentle mechanical stimulation to promote local blood circulation.
 
```
ESP8266 GPIO ──► 1kΩ ──► NPN 2N2222 ──► Coin Motor (3V, 10mm)
```
 
### 3. Linear Actuator
Physically tilts the head/foot section of the bed to fully shift patient weight.
 
```
ESP8266 ──► L298N Driver ──► Linear Actuator (12V, 100mm stroke)
```
 
### 4. Alert System
 
| Risk Level | Score | LED | Buzzer | App |
|------------|-------|-----|--------|-----|
| Safe | 0–39 | 🟢 Green | Off | — |
| Caution | 40–59 | 🟡 Yellow | Off | Info |
| Danger | 60–79 | 🔴 Red | Off | Push alert |
| Critical | 80–100 | 🔴 Flashing | On | CRITICAL alert |
 
---
 
## 🧠 AI & Algorithms
 
### Layer 1 — Moving Average Filter
Smooths raw sensor readings to eliminate electrical noise spikes.
```cpp
int movingAvgFSR(int new_val) {
    fsr_history[ma_index] = new_val;
    ma_index = (ma_index + 1) % MA_WINDOW;  // Window = 10 samples
    int sum = 0;
    for (int i = 0; i < MA_WINDOW; i++) sum += fsr_history[i];
    return sum / MA_WINDOW;
}
```
 
### Layer 2 — Time Analysis
Tracks how long pressure has been sustained — duration is the real danger, not magnitude alone.
```cpp
// 1 hour sustained pressure → risk level 2
// 2 hours sustained pressure → risk level 3 (critical)
pressure_duration = (millis() - pressure_start_time) / 1000;
```
 
### Layer 3 — Rule-Based Engine
```cpp
IF pressure > 700 AND duration > 3600  →  DANGER
IF temperature > 37.5°C               →  CAUTION
IF SpO2 < 95%                         →  DANGER
IF SpO2 < 90%                         →  CRITICAL
IF moisture detected                   →  CAUTION
```
 
### Layer 4 — Decision Tree (Multi-Factor Score)
 
```
Score = Pressure(0–40) + Duration(0–25) + Immobility(0–20)
      + Temperature(0–10) + SpO2(0–10) + Moisture(0–5)
      = 0 – 100
```
 
### Layer 5 — TinyML (TensorFlow Lite on ESP8266)
A neural network trained on real patient data, compressed to run directly on the ESP8266 — no internet required for inference.
 
```
Input:  [fsr, temperature, humidity, heart_rate, spo2, duration]
Model:  Dense(16, relu) → Dense(8, relu) → Dense(4, softmax)
Output: [P(safe), P(caution), P(danger), P(critical)]
Size:   < 20 KB (INT8 quantized)
```
 
**Training pipeline:**
```bash
# 1. Collect data from ESP8266 serial port
python python/collect_data.py
 
# 2. Train TensorFlow model
python python/train_model.py
 
# 3. Convert to TinyML and generate model.h for Arduino
python python/convert_to_tflite.py
```
 
---
 
## ☁️ Cloud & App
 
### Firebase Realtime Database Structure
```json
{
  "patients": {
    "patient_001": {
      "latest": {
        "fsr_raw": 720,
        "temperature": 36.8,
        "humidity": 65.2,
        "heart_rate": 78,
        "spo2": 97.4,
        "risk_score": 55,
        "pressure_duration": 3600,
        "timestamp": 1718200000
      },
      "history": {
        "1718200000": { "...": "..." },
        "1718196400": { "...": "..." }
      }
    }
  }
}
```
 
### Blynk App Dashboard
 
| Virtual Pin | Widget | Data |
|-------------|--------|------|
| V0 | Gauge | FSR Pressure (0–1023) |
| V1 | Gauge | Temperature (°C) |
| V2 | Gauge | Humidity (%) |
| V3 | Gauge | Heart Rate (BPM) |
| V4 | Gauge | SpO2 (%) |
| V5 | Gauge | **Risk Score (0–100)** |
| V6 | LED | Moisture Alert |
| V7 | Label | Pressure Duration |
| V8 | Chart | Risk Score History |
| V9 | Button | Manual Bed Raise |
 
---
 
## 🔧 Hardware Build
 
### Complete Parts List
 
**Controller**
```
ESP8266 NodeMCU v3 (CH340G)          × 1     ~$3.50
Breadboard 830-point                  × 2     ~$4.00
Jumper wire kit (M-M, M-F, F-F)      × 1     ~$2.50
```
 
**Sensors**
```
FSR 402 pressure sensor               × 3     ~$7.00
DHT22 temperature/humidity            × 1     ~$2.00
MPU-6050 GY-521 motion sensor         × 1     ~$1.20
Velostat pressure matrix 30×30cm      × 1     ~$4.00
Load cell 50kg + HX711 amplifier      × 4     ~$8.50
MAX30102 SpO2 + heart rate            × 1     ~$2.00
Capacitive moisture sensor            × 2     ~$2.00
Piezo disc 27mm + bridge rectifier    × 4     ~$1.70
```
 
**Actuation**
```
DC 12V mini air pump                  × 2     ~$8.00
Solenoid valve 12V NC                 × 4     ~$11.00
Inflatable air bladder 20×20cm        × 4     ~$10.00
Coin vibration motor 10mm×3mm 3V      × 6     ~$2.50
Linear actuator 12V 100mm             × 1     ~$11.00
L298N motor driver                    × 1     ~$1.50
4-channel relay module (active LOW)   × 1     ~$2.00
Active buzzer 5V + LEDs               × 1     ~$0.80
```
 
**Power**
```
12V 5A DC power supply                × 1     ~$7.00
LM2596 buck converter (12V → 5V)      × 1     ~$0.80
Capacitors, diodes, resistors kit     × 1     ~$3.50
```
 
**Total: ~$95 – $140 USD**
 
---
 
### Pin Allocation (ESP8266 NodeMCU)
 
```
D1 (GPIO5)  ──►  I2C SCL  (MPU6050 + MAX30102 + HX711)
D2 (GPIO4)  ──►  I2C SDA  (MPU6050 + MAX30102 + HX711)
D3 (GPIO0)  ──►  DHT22 data
D4 (GPIO2)  ──►  Buzzer
D5 (GPIO14) ──►  Relay IN1  (Air pump 1)
D6 (GPIO12) ──►  Relay IN2  (Air pump 2 / solenoids)
D7 (GPIO13) ──►  Relay IN3  (Actuator direction A)
D8 (GPIO15) ──►  Relay IN4  (Actuator direction B)
D0 (GPIO16) ──►  LED array
A0          ──►  FSR 402   (via voltage divider)
3V3         ──►  All sensor VCC
GND         ──►  Common ground
```
 
---
 
## 💻 Software Setup
 
### Prerequisites
- Arduino IDE 2.x with ESP8266 board support
- Python 3.10+
- TensorFlow 2.x
### Arduino IDE — Add ESP8266 Board
1. Open **File → Preferences**
2. Add to *Additional Boards Manager URLs*:
   ```
   http://arduino.esp8266.com/stable/package_esp8266com_index.json
   ```
3. **Tools → Board → Boards Manager** → search `esp8266` → Install
### Install Required Libraries
```
DHT sensor library          (Adafruit)       — Library Manager
Adafruit Unified Sensor     (Adafruit)       — Library Manager
MPU6050                     (Electronic Cats) — Library Manager
MAX30105                    (SparkFun)        — Library Manager
HX711 Arduino Library       (Bogdan Necula)   — Library Manager
FirebaseESP8266             (Mobizt)          — Library Manager
BlynkSimpleEsp8266          (Blynk)           — Library Manager
ArduinoJson                 (Benoit Blanchon) — Library Manager
TensorFlowLite_ESP8266      — Manual ZIP install
```
 
### Project Structure
```
AI_Careon/
├── AI_Careon.ino        ← Main firmware (upload this)
├── config.h             ← WiFi / Firebase / Blynk credentials
├── sensors.h            ← All sensor reading functions
├── algorithms.h         ← Moving avg · time analysis · decision tree
├── actuators.h          ← Air pump · vibration · linear actuator
├── cloud.h              ← Firebase + Blynk integration
├── model.h              ← TinyML model (auto-generated)
└── python/
    ├── collect_data.py       ← Log training data from serial
    ├── train_model.py        ← Train TensorFlow model
    └── convert_to_tflite.py  ← Export to TinyML + generate model.h
```
 
### Quick Start
 
**1. Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/ai-careon.git
cd ai-careon
```
 
**2. Configure credentials**
```cpp
// config.h
#define WIFI_SSID     "YourNetworkName"
#define WIFI_PASS     "YourPassword"
#define FIREBASE_HOST "yourproject.firebaseio.com"
#define FIREBASE_AUTH "your_firebase_secret_key"
#define BLYNK_AUTH    "your_blynk_token"
```
 
**3. Upload firmware**
```
Tools → Board → NodeMCU 1.0 (ESP-12E Module)
Tools → Upload Speed → 115200
Tools → Port → (your COM port)
Sketch → Upload
```
 
**4. Train the ML model** *(optional — system works without it)*
```bash
pip install tensorflow scikit-learn pandas joblib pyserial
python python/collect_data.py     # collect for several hours
python python/train_model.py      # train the model
python python/convert_to_tflite.py # deploy to ESP8266
```
 
**5. Open Serial Monitor** (115200 baud) to verify readings:
```
AI Careon v1.0 starting...
System ready!
FSR:320 Temp:36.8 Hum:62.1 HR:76 SpO2:98.0 Score:12 Time:0s
FSR:318 Temp:36.8 Hum:62.3 HR:75 SpO2:97.8 Score:12 Time:5s
```
 
---
 
## 📊 Results & Impact
 
### Clinical Value
 
| Benefit | How AI Careon Achieves It |
|---------|--------------------------|
| Detect Stage 1 before progression | Real-time pressure + time monitoring triggers intervention before irreversible damage |
| Reduce ICU bed sore rates | Automated actuation compensates when nurses cannot reposition every 2 hours |
| Reduce hospital stays | Bed sores add 5–30 extra days of hospitalization on average |
| Prevent life-threatening infection | Stage 4 ulcers can cause sepsis — prevention eliminates the risk |
| Remote patient monitoring | Firebase + Blynk enable caregivers to monitor from anywhere |
 
### Cost Comparison
 
```
Commercial alternating-pressure mattress system:    $2,000 – $8,000
Medical-grade pressure monitoring system:           $5,000 – $20,000
─────────────────────────────────────────────────────────────────────
AI Careon (complete build):                            ~$95 – $140
─────────────────────────────────────────────────────────────────────
Cost savings:                                              96–99%
```
 
### System Specifications
 
| Specification | Value |
|---------------|-------|
| Sampling rate | Every 5 seconds |
| Cloud upload rate | Every 30 seconds |
| Alert response time | < 1 second (local) |
| WiFi range | Standard 2.4 GHz (~50m) |
| Power consumption | ~800mA @ 5V (sensors) + 12V for actuators |
| Operating temperature | 0–50°C |
| Risk score range | 0–100 (composite multi-factor) |
| ML model size | < 20 KB (TFLite INT8 quantized) |
 
---
 
## 👥 Team
 
| Role | Responsibility |
|------|---------------|
| **Programmer** | ESP8266 firmware · AI algorithms · Firebase · Blynk · TinyML |
| **Hardware Engineer** | Circuit design · sensor integration · actuator wiring |
| **Medical Advisor** | Clinical requirements · risk thresholds · patient safety |
| **Project Lead** | System architecture · testing · documentation |
 
---
 
## 📄 License
 
This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
 
---
 
## 🙏 Acknowledgements
 
- [NPIAP](https://npiap.com/) — National Pressure Injury Advisory Panel for clinical staging standards
- [Adafruit](https://adafruit.com/) — Sensor libraries
- [SparkFun](https://sparkfun.com/) — MAX30102 library
- [Blynk](https://blynk.io/) — IoT dashboard platform
- [Google Firebase](https://firebase.google.com/) — Realtime cloud database
- [TensorFlow Lite](https://www.tensorflow.org/lite) — On-device machine learning
---
 
<div align="center">
**Built with ❤️ to protect patients who cannot protect themselves**
 
<br/>
*If this project helped you, please ⭐ star the repository*
 
<<<<<<< HEAD
</div>
=======
</div>
>>>>>>> 5cd37dee896bda6fb84e9fd151dd337b62ddc980
