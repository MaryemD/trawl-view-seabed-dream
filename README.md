# Smart Trawl Gear Uplifting System Dashboard 🌊

A real-time, responsive web dashboard for monitoring and controlling trawl gear during fishing operations. Designed to enhance gear safety, optimize seabed interaction, and enable smart automation using sensor and GPS data.

![Dashboard Preview](./screenshot.png) <!-- Replace with actual image path if available -->

---

## 🚀 Features

- 🎯 **Real-Time Monitoring**
  - Continuous seabed distance tracking with gyroscopic corrections
  - Live sensor data via MQTT/WebSocket

- 🧠 **Smart Automation**
  - Autonomous gear lifting when seabed distance < 1.0m
  - Manual override via interactive UI controls

- 📊 **Animated Visualizations**
  - Dynamic trawl net and boat animation
  - Color-coded seabed proximity (Red: Danger, Yellow: Caution, Green: Safe)

- 🗺️ **GPS & Mapping**
  - Real-time boat tracking with Leaflet.js
  - Depth overlays and historical movement trails

- 🚨 **Alert System**
  - Warnings for proximity breaches and maintenance schedules

---

## 🧱 Software Stack

| Layer          | Technologies Used                                                                 |
|----------------|-------------------------------------------------------------------------------------|
| **Frontend**   | React.js (v18), Tailwind CSS (v3), ShadCN UI, Framer Motion, React Konva, Leaflet.js |
| **Comm. Layer**| MQTT.js, WebSocket, Mosquitto MQTT Broker                                          |
| **Backend**    | Node.js, Firebase Realtime Database & Hosting (AWS DynamoDB as alternative)        |
| **Visualization** | Canvas API, SVG Graphics                                                       |

---

## 📐 System Architecture

```mermaid
graph TD
  A[Sensor Data (Distance, GPS, Gyro)] --> B[MQTT/WebSocket Listener]
  B --> C[Logic Evaluation (Thresholds)]
  C --> D[UI Rendering (Boat, Net, Labels)]
  C --> E[Alert System (Warnings, Maintenance)]
  D --> F[User Interface (Manual Input)]
  F --> G[MCU/Winch Control]
