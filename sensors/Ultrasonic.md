# HC-SR04 Ultrasonic Sensor Lab

## Overview
The HC-SR04 is an ultrasonic distance sensor that measures the distance to an object by emitting a high-frequency sound pulse and measuring the time it takes for the echo to return.

The sensor works in two steps:
1. A short ultrasonic burst is sent out via the **Trigger** pin.
2. The **Echo** pin goes high for the duration of time it takes the sound to travel to the object and back. This time can be used to calculate distance.

![HC-SR04 Ultrasonic Sensor](https://raw.githubusercontent.com/zotbins/zotbins-project/main/images/ultrasonic.png)

---

## Wire Descriptions
| Pin | Label | Description |
|-----|-------|-------------|
| 1 | VCC | 5V Input Voltage |
| 2 | TRIG | Trigger Input — send a 10µs HIGH pulse to start a measurement |
| 3 | ECHO | Echo Output — goes HIGH for the duration of the return pulse |
| 4 | GND | Reference Ground |


>  **Note:** The HC-SR04 operates at 5V, but the Raspberry Pi's GPIO pins are 3.3V logic. A **voltage divider** must be used on the ECHO pin to step the signal down from 5V to 3.3V to avoid damaging the Pi.
>
> For full specifications, refer to the [HC-SR04 datasheet](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf).
---
## Voltage Divider for the ECHO Pin
 Since the ECHO pin outputs 5V and the Raspberry Pi GPIO only tolerates 3.3V, use a simple resistor voltage divider:
| Connection | Resistor | To |
|------------|----------|----|
| ECHO pin → | 1kΩ | GPIO input pin |
| GPIO input pin → | 2kΩ | GND |
This brings the 5V signal down to approximately 3.3V, which is safe for the Pi.
 ![Voltage Divider](https://raw.githubusercontent.com/zotbins/zotbins-project/main/images/voltage_divider.png)

---
## Distance Calculation
The speed of sound in air is approximately **343 m/s** (34300 cm/s). Since the pulse travels to the object and back, the distance is:

```
Distance (cm) = (Echo pulse duration in seconds × 34300) / 2
```
---
## Task
### 1. Circuit Setup
Set up the circuit on a breadboard
1. Connect **VCC** (pin 1) to the 5V rail.
2. Connect **GND** (pin 4) to the ground rail.
3. Connect **TRIG** (pin 2) to a GPIO output pin on the Raspberry Pi.
4. Connect **ECHO** (pin 3) through a voltage divider to a GPIO input pin on the Raspberry Pi.
---
### 2. Python Code
Write a Python program that continuously measures and prints the distance to the nearest object in centimeters.

Rather than handling the low-level timing manually, use a library to simplify the implementation. A commonly used option for the Raspberry Pi is **`gpiozero`**, which has built-in support for the HC-SR04 via its `DistanceSensor` class. Look up the documentation and use it to continuously read and print distance values at regular intervals.
