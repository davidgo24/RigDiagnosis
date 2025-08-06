# Gameplan and Planning (PRD/Sprints)

---

# 📄 RigDiagnosis – Product Requirements Document (PRD)

## 🧠 Overview

**FaultMate** is a mobile-first diagnostic assistant for truckers and small fleet owners. It connects via Bluetooth to a truck’s OBD dongle, reads engine fault codes (DTCs), explains them in plain English, and stores the fault history locally and in the cloud.

---

## 💥 Problem

Independent truckers and small fleets often:

- See engine fault codes (like `P203F`) they don’t understand
- Can’t access dealership-level tools
- Waste time/money reacting blindly
- Have no clean record of fault history

---

## 🎯 Solution

A mobile app that:

- Connects to a truck's BLE-compatible OBD dongle
- Reads DTC fault codes in real time
- Translates them into clear language with severity guidance
- Stores recent codes locally and in the cloud
- Alerts the driver when a new issue appears

---

## 🔑 Core Features (MVP)

| Feature | Description |
| --- | --- |
| 🔌 BLE Dongle Connection | Pair with Veepeak BLE+ or OBDLink MX+ |
| 🧾 Fault Code Reader | Read active DTCs from ECM |
| 💬 Plain English Code Explainer | Use local map or GPT (future) |
| 🚦 Severity Indicator | Color-coded: Green, Yellow, Red |
| 🧠 Fault History | Save last 5–10 faults locally + via API |
| 📲 Push Notifications | Notify when *new* fault is detected |
| 📤 FastAPI API Sync | POST scans to backend, fetch history |
| 🛠 Test Mode | Simulate faults when no dongle present |

---

## ❌ Out of Scope (For MVP)

- No login/authentication (API key-based only)
- No multi-user/fleet dashboard (post-MVP)
- No regen/reset/bi-directional controls yet
- No real-time GPS tracking

---

## 🧱 Tech Stack

| Layer | Tech | Purpose |
| --- | --- | --- |
| **Mobile App** | React Native + Expo | BLE + UI |
| **Bluetooth API** | `react-native-ble-plx` | Connect to OBD |
| **Local Storage** | `AsyncStorage` | Store scan history offline |
| **Notifications** | Expo Push Notifications | Local/mobile alerts |
| **Backend API** | FastAPI (Python) | REST endpoints for logs |
| **Database** | PostgreSQL (via Railway or Supabase) | Fault record storage |
| **API Client** | Axios or Fetch | POST scans from app |
| **DevOps** | Railway/Supabase | Easy deploy, dev DB |
| **Testing** | Real truck w/ BLE dongle + mock mode | End-to-end validation |

---

## 📆 Final 5-Week Sprint Plan

### ⏱ Time Commitment:

- ~1 hour/day, ~7–10 hours/week combined
- Isaac: data, truck logic, test UX
- David: code architecture, BLE, backend

---

### 🚀 Week 1 – BLE Pairing + Test Mode

> Get the app connected to the dongle (or sim mode)
> 

| Tasks | Owner |
| --- | --- |
| Set up React Native project | David |
| Install and test `react-native-ble-plx` | David |
| Scan and pair with BLE dongle | David |
| Add toggle for “Test Mode” | Shared |
| Log all connection success/failure | David |
| Review PID `03` spec for fault code | Isaac |

✅ **Definition of Done**:

BLE dongle pairs successfully OR fake test code loads in Test Mode.

---

### ⚙️ Week 2 – Read Fault Codes + Show Raw

> Pull DTCs from truck or mock source, display raw P-codes
> 

| Tasks | Owner |
| --- | --- |
| Send BLE command to get DTCs (`03`) | David |
| Decode hex into readable P-codes | David |
| Create basic `FaultCard` UI component | David |
| Build initial fault code JSON map | Isaac |
| Add fake response for test mode | Shared |

✅ **Definition of Done**:

P-code appears onscreen in-app after scan (real or simulated).

---

### 💬 Week 3 – Explain Codes + Show Severity

> Translate raw codes into friendly messages
> 

| Tasks | Owner |
| --- | --- |
| Add lookup table for 50–100 codes | Isaac |
| Tag each code with severity tier | Isaac |
| Show fault message in card w/ color UI | David |
| Build "Safe to Drive?" logic box | Shared |

✅ **Definition of Done**:

Driver sees fault explanation + red/yellow/green severity rating.

---

### 🧠 Week 4 – FastAPI Backend + Cloud Sync

> Enable cloud storage of fault history
> 

| Tasks | Owner |
| --- | --- |
| Set up FastAPI project | David |
| Create models: `Scan`, `Truck`, `Code` | David |
| Add `/scan` POST + `/history` GET | David |
| Store scans in PostgreSQL | David |
| From app, POST scan after reading | Shared |
| Add minimal auth (API key header) | David |

✅ **Definition of Done**:

Scans are stored remotely and retrievable via API.

---

### 🔔 Week 5 – Notifications + Real Testing

> Get push alerts working and test on a real truck
> 

| Tasks | Owner |
| --- | --- |
| Add Expo push notification setup | David |
| Trigger push on *new* fault | David |
| Log faults in Isaac’s real truck | Isaac |
| Review real-world phrasing w/ truckers | Isaac |
| Clean UI, prep demo | Shared |
| Record short demo video | Shared |

✅ **Definition of Done**:

Push alert fires on new fault + real truck test confirms working scan.

---

## 🧪 Success Criteria (MVP Complete)

| Goal | Metric |
| --- | --- |
| App connects to real BLE dongle | ✅ Confirmed with at least 1 truck |
| Fault code is translated & colorized | ✅ Driver understands the message |
| Scan is stored locally and remotely | ✅ Seen in PostgreSQL via API |
| Push notification triggers cleanly | ✅ Fired on first detection of new fault |
| Real-world feedback is positive | ✅ 2–3 truckers would actually use this |

---

###