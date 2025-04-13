# Smart Trawl Gear Uplifting System Dashboard

This project is a real-time dashboard designed to support intelligent, sensor-guided control of trawl fishing gear. It provides live feedback on seabed distance, automated lifting logic, animated gear visualization, and GPS tracking to ensure safer and more efficient trawling operations.

Developed with a modern web stack and real hardware sensor inputs, the system is suitable for both research and operational deployment aboard vessels.

---

## Overview

The dashboard allows fishing operators or automated systems to monitor and control the trawl net based on proximity to the seabed. The system receives real-time data from physical sensors (depth sonar, GPS, gyroscope), processes them, and responds visually and logically to ensure the net stays in safe operating zones.

It supports both manual and autonomous winch control modes. In autonomous mode, the system lifts the net when the seabed distance falls below a threshold.

---

## Core Features

### Real-Time Monitoring

- Continuous seabed distance updates using depth sensors and gyroscopic correction
- Color-coded safety zones: red (< 1.0m), yellow (1.0–1.5m), green (> 1.5m)
- Live animation of boat and trawl gear using React Konva

### Autonomous and Manual Net Control

- Autonomous mode uses defined thresholds to trigger winch control automatically
- Manual mode provides Lift/Lower buttons in the dashboard UI
- Toggle interface allows switching between modes in real-time

### GPS-Enhanced Visualization

- Interactive map showing current boat location and historical tracks
- Highlighted danger zones and bathymetric overlays using Leaflet.js
- Depth-aware visual feedback based on GPS position

### Alert and Logging System

- Maintenance, proximity, and emergency warnings shown in a real-time log
- Alerts tied to live data inputs and time-stamped
- Notification system updates when thresholds are crossed or manual overrides occur

---

## System Architecture

The dashboard uses a modular design, separating sensor ingestion, logic processing, UI rendering, and hardware command output.

### Data Flow

- Sensor values (distance, GPS, gyroscope) are published to a Mosquitto MQTT broker
- The frontend listens using MQTT.js or WebSocket and updates the internal state
- Logic layer checks values against thresholds (`minDistance = 1.0m`, `minSafeDistance = 1.5m`)
- The UI displays updated visuals and system status
- In automatic mode, the system issues net lift/lower commands when thresholds are crossed
- In both modes, users can manually lift/lower via control panel

---

## Software Stack

| Layer            | Technology Stack                                                            |
|------------------|------------------------------------------------------------------------------|
| Frontend         | React.js (v18), Tailwind CSS (v3), React Konva, ShadCN UI, Leaflet.js       |
| Communication    | MQTT.js, WebSocket, Mosquitto MQTT Broker                                   |
| Backend/Cloud    | Node.js, Firebase Realtime Database, Firebase Hosting, AWS DynamoDB (alt)   |
| Visualization    | Canvas API, SVG, React Konva for animations                                 |

---

## Hardware Components (Used in Live System)

- **Depth Sensor**: Measures seabed distance in real time (e.g., sonar-based sensor)
- **Gyroscope**: Used to correct angle-based error in depth readings
- **GPS Module**: Supplies geolocation for map tracking and depth-aware decisions
- **MCU (Microcontroller Unit)**: Receives dashboard commands to actuate winch motors
- **Winch Actuator**: Mechanically lifts or lowers the trawl net based on system input

---

## Live Gear Visualization

The dashboard is divided into four main interface zones:

1. **Gear Animation View** – Shows live boat, sensor, and trawl net with seabed distance visualization  
   ![Dashboard Overview](./assets/dashboard-overview.png)

2. **Control Panel** – Manual Lift/Lower buttons and autonomous mode toggle  
   ![Emergency Lifting Mode](./assets/emergency-lifting.png)

3. **System Logs** – Scrollable list of alert messages with timestamps  
   *Included in dashboard screenshot above*

4. **Map View** – Interactive map with real-time position, historical track, and seabed overlay  
   *Included in dashboard screenshot above*

Additional example during near-emergency:  
![Seabed Warning - 1.4m](./assets/seabed-warning.png)

---

## Local Development

### Prerequisites

- Node.js and npm
- MQTT Broker (e.g., Mosquitto)
- Firebase project (for database and optional hosting)

### Installation Steps

```bash
git clone https://github.com/OmarChouchane/trawl-view-seabed-dream.git
cd trawl-view-seabed-dream

npm install
