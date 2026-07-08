# 🏠 Arduino Based Smart Home System

### Integrated Automation and Security System using Arduino Uno

Simulated and Designed in Tinker CAD

---

## 📖 Overview

This project presents the design and simulation of an **Arduino Uno based Smart Home System** that integrates multiple automation and security sub-systems into a single, unified platform. The system automates door locking/unlocking, fan speed control, and room lighting, while also monitoring for security and safety hazards through motion and gas detection. All sensor readings and system statuses are displayed in real time on a 16x2 I2C LCD and printed to the Serial Monitor for debugging and verification.

The complete system was designed, wired, and simulated using **Tinker CAD**, with results confirming reliable automated responses across all sub-systems.

---

## 🎯 Objectives

- 🔒 Design an automatic door locking and unlocking mechanism using an ultrasonic sensor and servo motor
- 🌡️ Implement automatic fan speed control based on real-time temperature readings using a DC motor
- 💡 Design an automatic room lighting system that responds to ambient light levels using an LDR
- 📟 Integrate a 16x2 I2C LCD for real-time visual display of all sensor readings and system status
- 🚨 Implement a PIR motion-based security alert system for a secret locker door
- 🔥 Implement a gas leak detection and alert system using an MQ2 gas sensor
- ✅ Simulate and validate the complete integrated system using Tinker CAD

---

## 🔧 Project Features

| Feature | Sensor / Component | Description |
|---|---|---|
| 🔒 Door Locking System | Ultrasonic (HC-SR04) + Servo | Auto lock/unlock based on proximity |
| 🌡️ Fan Speed Control | LM35 Temperature Sensor | 3-speed PWM fan control based on temperature |
| 💡 Room Lighting Control | LDR | Auto ON/OFF lighting based on ambient light |
| 🚨 Motion Security Alert | PIR Sensor | Detects unauthorized motion near a secret locker |
| 🔥 Gas Detection | MQ2 Gas Sensor | Detects LPG/smoke leakage in the kitchen |
| 📟 LCD Display | 16x2 I2C LCD | Real-time cycling display of all system statuses |
| 🖥️ Serial Monitor | Arduino IDE | Mirrors all sensor readings for debugging |

---

## 🧰 Components Used

- Arduino Uno
- HC-SR04 Ultrasonic Distance Sensor
- Servo Motor
- LM35 Temperature Sensor
- DC Motor (Fan) with NPN Transistor Driver + Flyback Diode
- LDR (Light Dependent Resistor) + 10kΩ Resistor
- LED (Room Light Indicator)
- 16x2 I2C LCD Display (PCF8574-based)
- PIR Motion Sensor
- MQ2 Gas Sensor
- Piezo Buzzer (shared for PIR and Gas alerts)

---

## 🏡 Sensor Placement in the House

| Sensor | Location | Purpose |
|---|---|---|
| Ultrasonic Distance Sensor (HC-SR04) | Main entrance door, facing outward | Detects approaching person to trigger door lock/unlock |
| PIR Motion Sensor | Near the secret locker door | Detects unauthorized motion in restricted area |
| Gas Sensor (MQ2) | Kitchen, near cooking/gas stove area | Monitors for LPG or smoke leakage |
| LDR (Light Sensor) | Near a window or main living area ceiling | Controls room light based on brightness |
| LM35 Temperature Sensor | Interior wall of living room/bedroom | Senses ambient temperature for fan control |
| 16x2 I2C LCD Display | Central, easily visible location | Displays all system statuses at a glance |
| Buzzer | Central location | Audible for both locker and kitchen alerts |

---

## ⚙️ System Overview

The system is built around a central **Arduino Uno** microcontroller that interfaces with all sensors and actuators. Each sub-system operates independently within the main control loop — continuously reading sensor values, taking automated decisions, and updating outputs (servo position, motor speed, LED and buzzer states) accordingly. The 16x2 I2C LCD cycles through five information screens — Door status, Light status, Fan status, Gas status, and Locker Motion status — refreshing continuously alongside identical output on the Serial Monitor.

---

## 🔌 Circuit Design and Connections

### 1. Automatic Door Lock/Unlock (Ultrasonic Sensor + Servo)

An HC-SR04 ultrasonic distance sensor continuously measures the distance of any object/person approaching the door. When the measured distance falls within the defined threshold, the servo motor rotates to the unlocked position; otherwise, it returns to the locked position.

| Component Pin | Arduino Pin |
|---|---|
| HC-SR04 VCC | 5V |
| HC-SR04 GND | GND |
| HC-SR04 Trig | D9 |
| HC-SR04 Echo | D10 |
| Servo Signal | D6 |
| Servo VCC | 5V |
| Servo GND | GND |

### 2. Automatic Fan Speed Control (LM35 + DC Motor)

An LM35 temperature sensor provides an analog voltage proportional to the ambient temperature. This is converted to degrees Celsius and used to switch the DC motor (fan) between OFF, MEDIUM, and FULL speed using PWM through an NPN transistor driver circuit, with a flyback diode protecting the circuit from back-EMF.

| Component Pin | Arduino Pin |
|---|---|
| LM35 VCC | 5V |
| LM35 Vout | A1 |
| LM35 GND | GND |
| Transistor Base (via 1kΩ) | D3 (PWM) |
| Transistor Emitter | GND |
| Transistor Collector | Motor (−) terminal |
| Motor (+) terminal | 5V |
| Diode (flyback, parallel to motor) | Cathode–5V, Anode–Collector |

### 3. Automatic Light Control (LDR + LED)

A photoresistor (LDR) forms a voltage divider with a 10kΩ resistor. As ambient light decreases, the LDR's resistance increases, lowering the voltage sensed at the analog pin. When this value drops below a defined threshold, the LED (representing the room light) is switched ON automatically.

| Component Pin | Arduino Pin |
|---|---|
| LDR Leg 1 | 5V (via divider) |
| LDR Leg 2 / 10kΩ junction | A0 |
| 10kΩ Resistor (other leg) | GND |
| LED Anode (through 220Ω) | D8 |
| LED Cathode | GND |

### 4. 16x2 I2C LCD Display

A PCF8574-based I2C LCD module displays real-time sensor readings and status for all sub-systems, cycling through multiple screens with a short delay between each.

| Component Pin | Arduino Pin |
|---|---|
| LCD I2C GND | GND |
| LCD I2C VCC | 5V |
| LCD I2C SDA | A4 |
| LCD I2C SCL | A5 |

### 5. PIR Motion Sensor + Buzzer (Secret Locker Alert)

A PIR sensor is mounted near a secret locker door. When motion is detected, the shared piezo buzzer sounds a single beep as an immediate audible alert, and the LCD/Serial Monitor display 'DETECTED! ALARM'.

| Component Pin | Arduino Pin |
|---|---|
| PIR VCC | 5V |
| PIR GND | GND |
| PIR OUT | D2 |
| Buzzer (+) | D4 |
| Buzzer (−) | GND |

### 6. Gas Sensor (MQ2) + Buzzer (Gas Leak Alert)

An MQ2 gas sensor continuously monitors the surrounding air quality. If the analog reading exceeds the calibrated safe threshold, the system interprets this as a gas leak and sounds the shared buzzer with a distinct two-beep pattern, differentiating it from the single-beep PIR alert.

| Component Pin | Arduino Pin |
|---|---|
| MQ2 Gas Sensor VCC | 5V |
| MQ2 Gas Sensor GND | GND |
| MQ2 Gas Sensor AO | A2 |

---

## 🧠 Working Principle / Logic Summary

### Door Lock Logic
The ultrasonic sensor continuously measures distance in centimeters. When the measured distance is less than or equal to 50 cm, the servo rotates to 90° (UNLOCKED); otherwise, it returns to 0° (LOCKED). This ensures the door remains secured by default and only opens when someone is genuinely present at close range.

### Fan Speed Logic (3 Conditions)
- Below 23°C → Fan OFF (PWM 0)
- 23°C to 33°C → Fan MEDIUM speed (PWM 128)
- 33°C and above → Fan FULL speed (PWM 255)

This three-tier response allows the fan to scale its output proportionally to actual thermal conditions rather than a simple binary ON/OFF.

### Light Control Logic
When the LDR reading falls below a threshold of 500, indicating insufficient light, the LED is switched ON automatically. When the reading is at or above 500, the LED stays OFF, avoiding unnecessary power consumption in well-lit conditions.

### Security Alert Logic (PIR and Gas Sensor)
Both the PIR and MQ2 sensors share the same buzzer but are distinguished by different beep patterns:
- **PIR detects motion** → single short beep + 'DETECTED! ALARM' on LCD
- **MQ2 detects gas leak** → distinct two-beep pattern
- **No detection** → buzzer held OFF

This allows a single shared buzzer to meaningfully communicate two entirely different categories of alerts, purely through sound pattern.

---

## 🧪 Simulation Results (Tinker CAD)

The following scenarios were verified during simulation:

- ✅ Door status switches to UNLOCKED when an object is detected within range
- ✅ Room light turns ON automatically under low ambient light
- ✅ Fan speed (PWM) increases progressively with rising temperature
- ✅ Gas leak detection triggers a 2-beep buzzer alert
- ✅ PIR motion near the locker triggers a 1-beep buzzer alert

---

## ✅ Conclusion

The Arduino Based Smart Home System successfully demonstrates the integration of multiple automation and safety sub-systems into a single, cohesive design. The door lock automatically responds to proximity, the fan speed adapts dynamically to ambient temperature, and the room light activates automatically in low-light conditions — reducing manual intervention and improving energy efficiency. The addition of PIR-based locker security and MQ2-based gas leak detection extends the system's utility beyond convenience into safety-critical monitoring, with distinct audible alert patterns allowing users to immediately identify the type of alert without needing to check a display. Overall, the project validates that a single low-cost microcontroller platform can effectively manage several independent smart-home functions simultaneously.

---

## 🚀 Future Scope

- 📱 Integration with a mobile application or IoT platform (e.g., Blynk, ThingSpeak) for remote monitoring and control
- 🔑 Addition of a keypad or RFID-based authentication for the door lock instead of simple proximity detection
- 🌡️ Use of a more precise temperature/humidity sensor (e.g., DHT22) for improved fan control accuracy
- 🗂️ Data logging of gas and motion events with timestamps for historical security analysis
- 🔨 Migration from simulation to a physical hardware prototype for real-world deployment and testing

---

## 👤 Author

**Mallampally Jayantha Siva Srinivas**
B.Tech, Electronics & Communication Engineering
GitHub: [MJSS-09](https://github.com/MJSS-09)
