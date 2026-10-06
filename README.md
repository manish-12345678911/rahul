# H8 EMS — Paramedic Crew Mobile PWA & High-Frequency GPS Telemetry Simulator
### Module Author: **Rahul** (Mobile Front-End & Telemetry Engineer)

---

## 1. Project & Module Overview
This repository contains the **Frontline Paramedic Mobile Progressive Web App (PWA) & Telemetry Simulator** of the H8 Emergency Medical Services (EMS) Platform, designed and implemented by **Rahul**.

Paramedics operating frontline emergency ambulances require a mobile application that works on smartphone touchscreens, provides immediate audio/haptic dispatch alerts, tracks physical device satellite GPS coordinates, and guides crews through a standardized **5-Stage Clinical Mission Stepper**.

```
                [ Mobile Smartphone Cockpit (Crew PWA) ]
                                   │
                   ┌───────────────┴───────────────┐
                   ▼                               ▼
       [ 5-Stage Mission Stepper ]     [ High-Frequency GPS Engine ]
        0: Dispatched                   HTML5 Geolocation API
        1: En Route to Scene            Bearing & Speed Calculation
        2: At Scene / Triage            1Hz Broadcast to Cloud
        3: Transporting
        4: Clinical Handover
                   │                               │
                   └───────────────┬───────────────┘
                                   ▼
                   [ Multithreaded Fleet Simulator ]
                    Simulates 14 Ambulance Units
                    Real-Time Movement on Jaipur Roads
```

---

## 2. Key Contributions by Rahul

### A. Paramedic Crew Mobile Tactical PWA (`src/crew-mobile-pwa/`)
- Built the mobile touch-optimized interface tailored for emergency smartphones and rugged tablets.
- Implemented visual indicators for ambulance classification (`ALS` — Advanced Life Support vs `BLS` — Basic Life Support).
- Added audio siren dispatches and device vibration feedback when a new emergency is assigned.
- Created pre-arrival trauma alert triggers allowing paramedics to transmit patient vital signs directly to the receiving hospital trauma bay.

### B. 5-Stage Mission Stepper Workflow
- Standardized the physical emergency response lifecycle into 5 tactile stages:
  1. **Dispatched**: Unit notified of incident type and coordinates.
  2. **En Route**: Ambulance rolling with emergency sirens and live turn-by-turn guidance.
  3. **At Scene**: Paramedics arrived, conducting on-site patient triage.
  4. **Transporting**: Patient stabilized in vehicle, heading to assigned hospital.
  5. **Clinical Handover**: Patient safely transferred to emergency resuscitation bay.

### C. Live Satellite GPS Telemetry Client (`src/demo-telemetry-client.js`)
- Uses the HTML5 `navigator.geolocation.watchPosition` API to capture mobile GPS coordinates.
- Computes vehicle speed in km/h and dynamic compass bearing angle ($0^\circ - 360^\circ$) to render vehicle heading arrows on central maps.

### D. Java Multithreaded Fleet Simulator (`src/telemetry-simulator/`)
- Developed a high-performance multithreaded simulator in Java 17.
- Simulates realistic vehicle movements for all 14 metropolitan ambulances across Jaipur roads.

---

## 3. Technology Stack
- **Mobile Frontend**: HTML5 PWA, CSS3 Mobile-First Responsive, Vanilla JavaScript
- **Geolocation API**: HTML5 Geolocation, Leaflet Mobile Tiles, WebSockets
- **Simulator Backend**: Java 17, Multithreading (Executors, Concurrent Collections), Maven
- **Telemetry Protocol**: JSON over WebSockets / HTTP REST (1Hz sampling rate)

---

## 4. Directory Structure
```
03_Rahul_Crew_Mobile_Telemetry/
├── README.md                          <-- You are here
├── run_module.bat                     <-- 1-Click runner for Rahul's module
└── src/
    ├── crew-mobile-pwa/               <-- Frontline Paramedic Mobile PWA Application
    │   └── index.html
    ├── telemetry-simulator/           <-- Java Multithreaded Ambulance Fleet Simulator
    │   ├── pom.xml
    │   └── src/main/java/com/h8/ems/simulator/
    └── demo-telemetry-client.js       <-- Standalone GPS Telemetry Streaming Client
```

---

## 5. How to Run & Test Rahul's Module

### Option 1: Mobile Paramedic Cockpit (1-Click Run)
1. Double-click `run_module.bat` or run:
   ```cmd
   python -m http.server 8083 --directory src/crew-mobile-pwa
   ```
2. Open your browser or smartphone at:
   ```
   http://localhost:8083/index.html
   ```
3. Test Login:
   - Select Call Sign: **`AMB-01`** (ALS Unit)
   - Passcode: **`crew123`**
4. Test Mission Stepper:
   - Advance through the stages from **Dispatched** $\rightarrow$ **En Route** $\rightarrow$ **At Scene** $\rightarrow$ **Transporting** $\rightarrow$ **Handover Complete**.
   - Notice live status updates and mission milestone timers.

### Option 2: Java Fleet Telemetry Simulator
```cmd
cd src\telemetry-simulator
mvn compile exec:java
```

---

## 6. Viva & Teacher Q&A Preparation (Questions Rahul Can Answer)

**Q1: What was your specific role in this group project?**
> *Answer*: "I was the Mobile Front-End and Telemetry Engineer. I developed the Paramedic Crew Mobile PWA interface, the 5-stage mission stepper workflow, the GPS geolocation streaming logic, and the Java multithreaded fleet telemetry simulator."

**Q2: What is the purpose of the 5-stage mission stepper?**
> *Answer*: "In emergency medical operations, dispatchers and hospitals need to know the exact operational state of every ambulance. The 5-stage stepper allows paramedics to update their status with a single tap on mobile, ensuring zero radio confusion between Dispatch, Crew, and Hospital."

**Q3: How does your module track ambulance movement?**
> *Answer*: "On real mobile devices, it uses the HTML5 Geolocation API with `enableHighAccuracy: true`. For testing when ambulances are parked, my Java simulator generates continuous GPS waypoints, computing instantaneous velocity and compass bearing."

**Q4: How does the crew alert the receiving hospital before arriving?**
> *Answer*: "During Step 3 ('Transporting'), the paramedic mobile cockpit includes a 'Send Pre-Arrival Trauma Alert' button. This transmits estimated arrival time and patient vitals to Niraj's Hospital ED Trauma Hub before the ambulance arrives."

---

## 7. How to Push This Module to Your Own GitHub
```bash
git init
git add .
git commit -m "Initial commit: Rahul - Paramedic Crew Mobile PWA & Telemetry Simulator"
git branch -M main
git remote add origin https://github.com/<your-username>/ems-crew-telemetry.git
git push -u origin main
```
