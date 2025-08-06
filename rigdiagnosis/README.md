# 🚛 RigDiagnosis

RigDiagnosis is a mobile-first diagnostic assistant for truckers and small fleet owners. It connects via Bluetooth to a truck’s OBD (J1939) dongle, reads fault codes, explains them in plain English, and logs them locally and to the cloud.

---

## 🧠 Project Structure

rigdiagnosis/
├── mobile-app/ # React Native + BLE interface
├── backend/ # FastAPI + PostgreSQL API
├── isaac-research/ # Fault code JSONs, trucking insights
├── docs/ # PRD, diagrams, planning
├── shared/ # (Optional) Shared data or logic
└── README.md # This file

---

## 📦 Tech Stack

- **Mobile App**: React Native (Expo) + `react-native-ble-plx`
- **Backend**: FastAPI + SQLModel + PostgreSQL
- **BLE Dongle**: SAE J1939 to Bluetooth Gateway (Copperhill)
- **Storage**: AsyncStorage (local), PostgreSQL (cloud)

---

## 🚧 Current Status

- [ ] BLE pairing (Veepeak or Copperhill)
- [ ] Test Mode (simulate fault codes)
- [ ] Fault code display UI
- [ ] Backend API scaffolding
- [ ] Fault history logging
- [ ] Push notification support


---

## 📁 Isaac Folder Guide

Isaac will be working in:
isaac-research/
├── fault-code-base.json # Central list of fault codes
├── notes.md # Trucking convos, hardware ideas
└── test-logs/ # Raw outputs, experiments

yaml
Copy
Edit

---

## 📄 Resources

- Copperhill BLE Dongle: https://copperhilltech.com/sae-j1939-to-bluetooth-gateway-module/
- J1939 Primer: https://copperhilltech.com/blog/an-introduction-to-the-sae-j1939-protocol/

---

## 💬 Contact

- Contact David or Isaac for questions. support@rigdiagnosis.com