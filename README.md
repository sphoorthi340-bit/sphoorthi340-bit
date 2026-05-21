<div align="center">

```
╔═══════════════════════════════════════════════════════════════╗
║   SHASHANK SPHOORTHI  ·  AIoT & Intelligent Systems Engineer  ║
║   Edge AI  ·  Embedded Systems  ·  Secure IoT Architecture    ║
╚═══════════════════════════════════════════════════════════════╝
```

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Shashank_Sphoorthi-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/shashank-sphoorthi/)
[![Email](https://img.shields.io/badge/Email-Sphoorthi340%40gmail.com-EA4335?style=flat-square&logo=gmail)](mailto:Sphoorthi340@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Coming_Soon-111827?style=flat-square&logo=github)](https://github.com/sphoorthi340-bit)
[![Location](https://img.shields.io/badge/📍-Hyderabad,_India-1f6feb?style=flat-square)](#)

</div>

---

## 👤 Who I Am

I'm a **3rd-year ECE undergraduate** (B.Tech, Class of 2028) at the intersection of **embedded hardware and artificial intelligence** — what the industry is beginning to call **AIoT**: intelligent systems that sense, reason, and act at the edge, without cloud dependency.

My work centres on a single, high-conviction thesis:

> *"The most impactful AI is the kind that runs on a ₹600 microcontroller in a flood-hit village with no internet — not the kind that lives in a data centre."*

Every project I build is a step toward this. My flagship system, **Sahayak**, proved this thesis at the Kaggle × Google DeepMind Gemma 4 Good Hackathon. My hardware roots run from **ESP32 firmware and sensor conditioning pipelines** to **FPGA acceleration on Basys 3 (Vivado)**.

I'm actively targeting **MS programs in Embedded Systems / AIoT / Intelligent Systems** (Germany · Singapore · USA, Fall 2027 intake) and **embedded AI internships** for Summer 2026.

---

## 🏗️ Featured Projects

### 🚨 Sahayak (सहायक) — Offline-First AIoT Disaster Response System
> *Kaggle × Google DeepMind "Gemma 4 Good" Hackathon, 2026*

[![Repo](https://img.shields.io/badge/GitHub-Sahayak-181717?style=flat-square&logo=github)](https://github.com/sphoorthi340-bit/sahayak)
[![Demo](https://img.shields.io/badge/Demo-YouTube-FF0000?style=flat-square&logo=youtube)](https://youtu.be/fTYM_cO4mZo?si=PV0i1dq9V3y_T1RN)
[![Stack](https://img.shields.io/badge/Stack-ESP32_%7C_Gemma_4_%7C_FastAPI_%7C_React-555?style=flat-square)](#)

A full-stack AIoT system purpose-built for disaster scenarios where cellular infrastructure collapses. Designed around the 2024 Wayanad Landslides — where towers failed within minutes — Sahayak keeps communities connected when everything else goes dark.

**Systems Architecture:**
```
[ESP32 Field Nodes] ──ESP-NOW Mesh──► [ESP32 Base Station]
        │  (self-healing, no router, MAC-layer only)        │
   OLED + Keypad                                    Serial / USB
   (Hardware fallback)                                      │
                                                    [FastAPI Backend]
                                                     SQLite · Python
                                                            │
                                                    [React PWA Dashboard]
                                                  EN / हिंदी / తెలుగు
                                                            │
                                          [Gemma 4 E4B via Ollama — LOCAL]
                                           (NDMA protocol grounding, offline)
```

**Key Engineering Decisions:**
- **ESP-NOW over Wi-Fi/BLE** — operates on Wi-Fi MAC layer, infrastructure-independent, ~$7/node
- **Gemma 4 E4B via Ollama** — runs fully offline on a local command station, no API calls
- **Self-healing mesh** — nodes reroute around failures autonomously using ESP32 RTOS
- **PWA with multilingual support** — degrades gracefully to hardware keypads if phones are lost
- **Software Simulation Mode** — full demo without physical hardware (double-click version badge)

**Impact:** 15× cheaper than traditional emergency broadcast infrastructure; targets 640,000+ underserved Indian villages lacking redundant cellular coverage.

---

### 🔐 Dual-Layer Encrypted Wireless Chat Terminal — ESP32 + AES-128 + ChaCha20
> *Performance Analysis of Software vs. Hardware-Accelerated Encryption*

[![Repo](https://img.shields.io/badge/GitHub-Encrypted_Chat_Terminal-181717?style=flat-square&logo=github)](https://github.com/sphoorthi340-bit/esp32-encrypted-chat)
[![Stack](https://img.shields.io/badge/Stack-ESP32_%7C_mbedTLS_%7C_ESP--NOW_%7C_C%2B%2B-555?style=flat-square)](#)

A completely localized, infrastructure-independent encrypted communication system on two ESP32 nodes. Built to empirically benchmark hardware-accelerated vs. software-based cryptography on a constrained microcontroller.

**Architecture Highlights:**
- **Transport:** ESP-NOW peer-to-peer (Wi-Fi MAC layer, zero infrastructure)
- **Engine 1 — AES-128-ECB (Hardware):** Via `mbedtls`, offloaded to ESP32's dedicated crypto accelerator silicon → measured **~46 µs** encrypt latency
- **Engine 2 — ChaCha20 (Software):** Pure ARX operations per RFC 8439, no padding overhead → measured **~6 µs** software execution baseline
- **Runtime switching:** Physical GPIO 4 toggle — live algorithm swap without reflash
- **T9 message composer** on a 4×4 matrix keypad; SSD1306 OLED output
- **Tamper demonstration mode:** deliberate wrong-key decryption to visually prove cryptographic integrity

**Benchmarking Result:** Hardware AES-128 achieves vastly superior throughput for block workloads; ChaCha20 demonstrates lower initialization latency for continuous streams — with µs-per-packet telemetry logged live to serial.

> *Scored 10/10 at first Project Expo review. Key hardware design decisions: channel 0 ESP-NOW, volatile bool ACK callbacks, avoidance of GPIO 2/5/15 strapping pins.*

---

### 🌡️ Analog Signal Conditioning Infrastructure for Thermal Transduction
> *Precision op-amp pipeline: LM35 → LM358 → RC Filter → ESP32 ADC → OLED*

[![Repo](https://img.shields.io/badge/GitHub-Signal_Conditioning-181717?style=flat-square&logo=github)](https://github.com/sphoorthi340-bit/analog-signal-conditioning)
[![Stack](https://img.shields.io/badge/Stack-ESP32_%7C_LM35_%7C_LM358_%7C_Arduino_C%2B%2B-555?style=flat-square)](#)

A four-stage analog signal conditioning pipeline that solves the core problem of direct ADC digitization of low-amplitude sensor outputs (10 mV/°C from LM35) — which causes quantization errors and zero-offset drift under noise.

```
[LM35 Sensor]──10mV/°C──►[LM358 Non-Inverting Amp]──►[RC Low-Pass Filter]──►[ESP32 12-bit ADC]──►[OLED]
  Transduction               Av = 1 + R1/Rf               Noise Suppression      Digitization       Display
                             maps to 0–5V range            + Load Isolation
```

**Design Focus:** Signal integrity engineering — gain formula derivation, RC corner frequency selection, and ADC scaling math. Validates the full pipeline from raw millivolt thermal output to noise-free Celsius readout.

---

### 💪 Project Rebuild — Modular Fitness & Mental Health Architecture (Flutter × Firebase)

[![Repo](https://img.shields.io/badge/GitHub-Project_Rebuild-181717?style=flat-square&logo=github)](https://github.com/sphoorthi340-bit/project-rebuild)
[![Stack](https://img.shields.io/badge/Stack-Flutter_%7C_Dart_%7C_Firebase_%7C_Firestore-555?style=flat-square)](#)

A component-driven Flutter application architected for real-time synchronization of physical metrics and mental well-being. Demonstrates cross-domain software engineering alongside hardware projects.

**Architecture Decisions:**
- Strict tab-domain separation (`dashboard`, `workouts`, `nutrition`, `journal`, `mobility`) — O(1) component rendering, no global state pollution
- Cloud Firestore for async localized document snapshots (e.g. `week_01` schema retrieval) — sustained 60fps under heavy DOM manipulation
- Custom "FIRE" dark theme with glassmorphism via `BackdropFilter` matrix blurring
- Full Auth, progress analytics, streak tracking, mood/energy journaling, workout scheduling

---

## 🛠️ Technical Stack

```
┌─────────────────────────────────────────────────────────┐
│  EMBEDDED & HARDWARE                                    │
│  ESP32-WROOM-32 · Arduino / PlatformIO · Basys 3 FPGA  │
│  Vivado (VHDL/Verilog) · LM35/LM358 · ESP-NOW          │
│  LoRaWAN (learning) · MQTT · I2C/SPI/UART               │
├─────────────────────────────────────────────────────────┤
│  SYSTEMS & SECURITY                                     │
│  mbedTLS · AES-128-ECB · ChaCha20 (RFC 8439)           │
│  RTOS concepts · Systems Architecture & Diagramming    │
├─────────────────────────────────────────────────────────┤
│  AI / ML (active learning)                              │
│  Python · TensorFlow Lite · Gemma 4 via Ollama         │
│  Edge AI deployment · Anomaly detection fundamentals   │
├─────────────────────────────────────────────────────────┤
│  SOFTWARE                                               │
│  C/C++ · Python · Dart/Flutter · FastAPI · React       │
│  Firebase/Firestore · SQLite · Git · Linux              │
└─────────────────────────────────────────────────────────┘
```

---

## 📍 Where I'm Headed

```
NOW (2026)          →    2027              →    2028+
─────────────────────────────────────────────────────────
Secure AIoT         →    MS Application   →    MS Abroad
Flagship Project         (GER/SGP/USA)         Embedded AI /
+ Internship             IELTS · SOP           Intelligent Systems
(Embedded/IoT)           LORs · CGPA ~8.2      → Systems Architect
                                               → Tech Consultant
```

**Target MS Programs:** Univ. of Freiburg (M.Sc. Embedded Systems) · TU Munich (Robotics/CPS) · TU Delft (Computer Eng.) · NTU Singapore (Robotics & Intelligent Systems) · RWTH Aachen · Georgia Tech ECE

**Target Internship Roles:** Embedded AI Engineer · IoT Systems Intern · Edge Computing Intern · Industrial Automation Intern
*(Bosch · Siemens · ABB · Infineon · NXP · Altizon · GovTech Singapore)*

---

## 📊 GitHub Stats

<div align="center">

![GitHub Streak](https://streak-stats.demolab.com?user=sphoorthi340-bit&theme=dark&hide_border=true&background=0d1117&stroke=58a6ff&ring=58a6ff&fire=58a6ff&currStreakLabel=58a6ff&sideLabels=58a6ff&dates=888888)

![Top Languages](https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=sphoorthi340-bit&theme=github_dark)
</div>

---

## 📫 Let's Connect

I'm always open to conversations about **edge AI, embedded systems architecture, IoT security, and AIoT research**. If you're working on something at the intersection of hardware and intelligence — reach out.

- 📧 **Email:** [Sphoorthi340@gmail.com](mailto:Sphoorthi340@gmail.com)
- 💼 **LinkedIn:** [linkedin.com/in/YOUR-LINK](https://www.linkedin.com/in/shashank-sphoorthi/)
- 🐙 **GitHub:** [@sphoorthi340-bit](https://github.com/sphoorthi340-bit)

---

<div align="center">

*"Build at the edge. Reason at the edge. Stay offline-first."*

![Visitor Count](https://komarev.com/ghpvc/?username=sphoorthi340-bit&color=58a6ff&style=flat-square&label=Profile+Views)

</div>
