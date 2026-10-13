**10/12/2026: Planning**  
Flight Controller will be built in versions for scalability.  
PCB V1 Requirements:
- Log altitude
- Log acceleration
- Log GPS position
- Detect apogee
- Fire parachute
- Radio live data to ground station
Later on, V2 will feature pitot tube to detect airspeed and calculate displacement.
| Component | Chip/module | Connects to Pico 2 by: | Function |
| -------- | -------- |
| Microcontroller | Raspberry Pi Pico 2 | soldered onto board | Runs MicroPython |
| Barometer | BMP390 | I2C | Altitude, apogee detection |
| IMU | LSM6DSO32 (±32 g) | I2C | Launch detection, acceleration |
| Logging | WS25Q128 flash | SPI | Stores every reading |
| Radio | RFM95W Lora, 915 MHz | SPI (own chip-select pin) | Sends telemetry down |
| GPS | u-blox M8/M10 breakout on headers| UART | Position, landing spot |
| Pyro channel | Logic-level MOSFET + arming switch | GPIO + ADC (continuity) | Fires the e-match |
| Buzzer, LEDs | Magnetic buzzer + transistor | GPIO | Status and finding the rocket |
| Power | 1S LiPo -> Schottky -> VSYS | ADC (battery voltage) | Pico's regulator makes 3.3 V |

Ground station: 
```
A second Pico 2 with an RFM95W, plugged into my laptop by USB
```

**Time Spent: 2 hours**
