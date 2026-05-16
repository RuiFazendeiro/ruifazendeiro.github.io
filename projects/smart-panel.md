---
layout: default
title: IoT Smart Electrical Panel
---

# IoT Smart Electrical Panel with Edge Energy Management
*Project developed for RVCC Electrotechnical Technician Level 4 (Passed with Distinction)*

## Project Overview
This project shifts the traditional electrical panel from a passive protection element to an active, intelligent node. Built entirely with industrial DIN-rail components, it integrates power electronics, embedded firmware, and IoT telemetry to manage energy consumption and optimize load distribution.

## Technical Architecture

### 1. Hardware & Infrastructure
* **Central Controller:** ESP32-S3-RS485-CAN, utilizing its native hardware interfaces to eliminate external transceiver fragmentation.
* **Telemetry Input:** Eastron SDM230 Modbus energy meter connected via RS485.
* **Actuators:** Solid State Relays (SSRs) for high-priority/low-priority AC loads and TRIAC-based AC phase dimming circuits.
* **Thermal Management:** Active proportional PWM cooling system driven by digital DS18B20 temperature sensors.

### 2. Embedded Firmware & Logic (C++)
* **Non-Blocking Execution:** Implemented using a cooperative polling architecture (via `millis()` timers) to ensure continuous sensor evaluation and safety checks without blocking execution loops.
* **Modbus RTU Telemetry:** Continuous polling of active power, current, and voltage parameters from the Eastron meter.
* **Autonomous Load-Shedding Algorithm:** Implemented an edge computing logic that monitors total active power. If consumption exceeds **3000W**, the controller automatically disconnects low-priority loads via SSRs. Reconnection occurs safely using a mathematical hysteresis threshold when power drops below **2500W**.

### 3. Safety by Design (Hardwired Layer)
* Independent of the microcode state, the system incorporates a physical hardwired safety layer. 
* A dedicated Emergency Stop (E-Stop) auto-retention circuit cuts critical actuator power instantly if triggered, ensuring hardware-level protection even during firmware failures or system lockups.

### 4. Connectivity & Interface
* **Embedded Web Server:** Serves a lightweight HTML/JavaScript dashboard hosted directly on the ESP32-S3 for real-time telemetry monitoring and manual 3-channel TRIAC dimming control over the local network.
* **CAD Documentation:** Engineered the complete electrical schematics, power distribution diagrams, and command circuits using AutoCAD.

📥 **[Download Technical Presentation (PDF)](/assets/Portefólio Técnico - Quadro IoT.pdf)**



[← Back to CV](/)
