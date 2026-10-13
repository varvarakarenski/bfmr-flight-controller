---
title: "Baby's First Model Rocket: Flight Controller"
author: "Varvara Karenski"
description: "KiCad and planning files for BFMR flight controller"
created_at: "2026-10-12"
---

# **October 12:** Planning

<img src="./images/oct12.jpg" width="300" alt="Chalkboard scrawlings">

Researched PCB flaws and tips, found inspo and design references, and safety protocols.

## Helpful Links

- https://github.com/The-Faulty/Lyra
- https://magazine.raspberrypi.com/articles/starlight-model-rocket-flight-computer-vs-rockit-flight-computer
- https://altusmetrum.org/EasyMini/
- https://nar.org/ModelRocketSafetyCode 
- https://www.nakka-rocketry.net/alti.html

Created Slack pitch in #forgery and organized all subprojects on forge hub.

I decided that the flight controller will be built in versions for scalability.

PCB V1 requirements:

- Log altitude
- Log acceleration
- Log GPS position
- Detect apogee
- Fire parachute
- Radio live data to ground station

Later on, V2 will feature a pitot tube to detect airspeed and calculate displacement.

| Component | Chip/module | Connects to Pico 2 by | Function |
| --------- | ----------- | --------------------- | -------- |
| Microcontroller | Raspberry Pi Pico 2 | Soldered onto board | Runs MicroPython |
| Barometer | BMP390 | I2C | Altitude, apogee detection |
| IMU | LSM6DSO32 (±32 g) | I2C | Launch detection, acceleration |
| Logging | W25Q128 flash | SPI | Stores every reading |
| Radio | RFM95W LoRa, 915 MHz | SPI (own chip-select pin) | Sends telemetry down |
| GPS | u-blox M8/M10 breakout on headers | UART | Position, landing spot |
| Pyro channel | Logic-level MOSFET + arming switch | GPIO + ADC (continuity) | Fires the e-match |
| Buzzer, LEDs | Magnetic buzzer + transistor | GPIO | Status and finding the rocket |
| Power | 1S LiPo -> Schottky -> VSYS | ADC (battery voltage) | Pico's regulator makes 3.3 V |

Ground station: a second Pico 2 with an RFM95W, plugged into my laptop by USB.

**Total time spent: 2 hours**
