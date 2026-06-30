# 🏥 CareOnAI V1: Autonomous Pressure Injury Prevention System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform: ESP32](https://img.shields.io/badge/Platform-ESP32-blue)](https://www.espressif.com/)
[![Cloud: Firebase](https://img.shields.io/badge/Cloud-Firebase-orange)](https://firebase.google.com/)
[![AI: TinyML](https://img.shields.io/badge/AI-TinyML-green)](https://www.tensorflow.org/lite/microcontrollers)

## 📌 Overview
**CareOnAI** is an autonomous, closed-loop embedded AI healthcare system designed to prevent pressure injuries (bed sores) in immobilized patients. Unlike passive mattresses, CareOnAI utilizes a network of sensors and a TinyML-powered edge device to detect ischemia risk in real-time and trigger an automated **Alternating Pressure Therapy (APT)** cycle.

The system bridges the gap between continuous clinical monitoring and automated actuation, reducing the burden on nursing staff while significantly improving patient outcomes.

---

## 🧬 Clinical Basis
The system is engineered around the **Capillary Closing Pressure (CCP)** principle. When pressure on a specific body area exceeds $\approx 32\text{ mmHg}$, blood flow is restricted, leading to tissue hypoxia and eventual necrosis.

**CareOnAI monitors three critical risk vectors:**
1. **Pressure (Ischemia):** Detected via a matrix of FSR (Force Sensitive Resistors).
2. **Microclimate (Maceration):** Monitored via SHT31-D sensors (Humidity $> 70\%$ RH increases skin fragility).
3. **Mobility (Stillness):** Tracked via MPU6050 Accelerometer/Gyroscope to detect lack of patient shifting.

---

## 🏗️ System Architecture

### 1. Hardware Layer (The Edge)
- **Controller:** ESP32 DevKit V1 (Dual-core, WiFi/BT).
- **Sensing Suite:** 
  - 6x FSR 402 (Pressure mapping).
  - SHT31-D (High-precision Temperature/Humidity).
  - MPU6050 (6-Axis Motion Tracking).
- **Actuation:** 12V DC Pump + Solenoid Valve Matrix for targeted bladder inflation/deflation.
- **Power:** LM2596 Buck Converter for stable 5V/3.3V rails.

### 2. Intelligence Layer (TinyML)
- **Model:** TensorFlow Lite Micro (int8 quantized).
- **Inference:** On-device classification of "Safe," "Caution," "Danger," and "Critical" states.
- **Adaptation:** Dynamic patient-baseline calibration to account for varying BMI and skin sensitivity.

### 3. Cloud & Monitoring Layer
- **Database:** Firebase Realtime Database (RTDB) for ultra-low latency data streaming.
- **Frontend:** React.js + Vite + Tailwind CSS.
- **Visualization:** Recharts for real-time pressure and humidity trending.

---

## 🚀 Key Features
- ✅ **Closed-Loop Automation:** Automatically triggers pressure shifts without human intervention.
- ✅ **Real-time Telemetry:** Live dashboard for medical staff to monitor multiple patients.
- ✅ **Patient-Specific Profiling:** Adjustable thresholds based on medical history (BMI, skin condition).
- ✅ **Non-Blocking Architecture:** Firmware implemented using a millisecond-based scheduler for high reliability.

---

## 🛠️ Tech Stack
| Component | Technology |
| :--- | :--- |
| **Firmware** | C++, Arduino Framework, ESP-IDF |
| **AI/ML** | TensorFlow Lite Micro, Python (Pandas, Scikit-Learn) |
| **Backend** | Firebase RTDB |
| **Frontend** | React, Vite, Tailwind CSS, Recharts |
| **Hardware** | ESP32, FSRs, SHT31, MPU6050, 12V Pneumatics |

---

## 🗺️ Roadmap
- [x] Clinical Specification & Logic Mapping.
- [x] Non-blocking Firmware Skeleton.
- [x] Firebase $\leftrightarrow$ React Pipeline.
- [ ] Hardware Integration & Sensor Calibration.
- [ ] Real-world Data Collection & Model Training.
- [ ] Full-scale Prototype Testing.

---

## ⚠️ Medical Disclaimer
*CareOnAI V1 is a prototype developed for research and competition purposes. It is NOT a certified medical device and should not be used for actual patient care without rigorous clinical trials and regulatory approval (FDA/CE).*
