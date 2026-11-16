# ADAS with Driver Intent Recognition (DIRS)

An embedded driver-assistance prototype that watches both the **road** and the **driver**. Firmware running on NodeMCU (ESP8266) and Arduino reads multiple sensors, works out the driver's turn intent, fatigue and distraction, and raises an alert in **under 32 ms**. Sensor data is also published over MQTT to Blynk and ThingSpeak for live remote monitoring.

Built as an internship project with the IEEE Sensors Council Kerala Chapter (June 2025).

## Why this project

A standard ADAS looks outward: lane, obstacles, speed. Many accidents, though, start with the driver: no signal before a turn, drowsiness, or a distracted glance. DIRS adds the driver side, so the system knows what the driver is about to do and whether they are in a fit state to do it.

## Features

- Real-time monitoring of lane, obstacles and speed
- Driver behaviour tracking: turn intent, fatigue and distraction
- On-device alert logic with response latency under 32 ms
- Sensor polling at about 10 Hz
- Wireless sensor network (WSN) publishing data over MQTT
- Live dashboard and logged history on Blynk and ThingSpeak

## System overview

```
 Sensors (road + driver)
        |
        v
 NodeMCU / Arduino  --->  Alert logic (runs on the microcontroller)
        |                          |
        | MQTT                     v
        v                   Driver alert (< 32 ms)
 Blynk / ThingSpeak
 (monitoring + history)
```

Safety alerts are decided in the firmware, not in the cloud, so they do not depend on Wi-Fi or a network round trip. The cloud side is only used for monitoring and analysis.

## Hardware

| Component | Role |
|---|---|
| NodeMCU (ESP8266) | Wi-Fi enabled controller, publishes data over MQTT |
| Arduino | Sensor reading and alert logic |
| TODO: sensor list | TODO: what each sensor measures (turn intent, fatigue, distraction, lane, obstacle, speed) |

## Software

- **Language:** Embedded C
- **Platforms:** NodeMCU / Arduino firmware
- **Protocols:** MQTT, with GPIO and serial communication between boards (TODO: confirm UART / I2C / SPI usage)
- **Cloud / IoT:** Blynk, ThingSpeak

## How it works

1. Sensors are polled at about 10 Hz.
2. The firmware processes the readings to track lane, obstacles and speed, and to detect turn intent, fatigue and distraction. (TODO: one line on how fatigue and distraction are detected.)
3. If a condition is unsafe, an alert is triggered immediately on the device.
4. In parallel, the NodeMCU publishes the readings over MQTT to Blynk and ThingSpeak.

## Results

- Alert response latency under **32 ms**
- Continuous real-time lane, obstacle and speed monitoring at about 10 Hz
- Live remote monitoring through Blynk and ThingSpeak

TODO: add how the 32 ms figure was measured.

## Getting started

```bash
git clone https://github.com/Madhav-M-6385/ADAS-DIRS.git
cd ADAS-DIRS
```

1. Open the firmware in the Arduino IDE (TODO: folder names for NodeMCU and Arduino sketches).
2. Install the required libraries (TODO: list, e.g. ESP8266 board package, PubSubClient, Blynk).
3. Set your Wi-Fi credentials, MQTT broker details and Blynk / ThingSpeak keys in the config section of the code. Never commit real keys.
4. Flash the sketches to the NodeMCU and Arduino and power the sensors.

## Repository structure

```
ADAS-DIRS/
|-- TODO: firmware folders
|-- TODO: circuit diagram / images
|-- README.md
```

## Future improvements

- A more reliable fatigue and distraction model
- Additional sensors for better driver monitoring
- Moving to an RTOS for stricter timing guarantees

## Author

**Madhav M**
ECE graduate, Rajagiri School of Engineering and Technology
[LinkedIn](https://linkedin.com/in/madhav-m-5953a0225) | [GitHub](https://github.com/Madhav-M-6385)
