# Breakbeam Sensor 
## Overview
The breakbeam sensor consists of two components:
-  **Emitter (black bulb):** Continuously shoots an infrared (IR) beam from its center.
-  **Receiver (clear bulb):** Detects the IR beam and outputs a binary signal indicating whether the beam is intact or broken.

When the beam path is unobstructed, the IR signal reaches the receiver and outputs **logic low (0V)**. When an object interrupts the beam, the receiver outputs **logic high (pulled to VCC: 3.3V–5V)**, signaling that the beam is broken.

![Breakbeam Sensor](https://github.com/zotbins/zotbins-project/blob/main/images/ir_2.png)

---
## Wire Descriptions
### Receiver

| Wire Color | Label | Description |
|------------|--------|---------------------------------------------------------|
| Red | VCC | 3.3V–5V Input Voltage |
| Black | GND | Reference Ground |
| White | Signal | Logic LOW (0V) = beam intact; Logic HIGH (VCC) = beam broken |

### Emitter
| Wire Color | Label | Description |
|------------|-------|-----------------------|
| Red | VCC | 3.3V–5V Input Voltage |
| Black | GND | Reference Ground |

>  **Note:** Both the receiver and emitter must share the same reference ground for the sensor to function correctly.
>
> For full specifications, refer to the [Adafruit IR Breakbeam datasheet](https://www.adafruit.com/product/2167).
---
## Task
### 1. Circuit Setup
Set up a basic circuit on a breadboard:

1. Connect the **emitter's** VCC (red) to 3.3V or 5V and GND (black) to ground.
2. Connect the **receiver's** VCC (red) to 3.3V or 5V and GND (black) to the **same** ground rail as the emitter.
3. Connect the **receiver's signal wire** (white) to a GPIO input pin on your microcontroller.
4. Align the emitter and receiver so they face each other with a clear line of sight.
---
### 2. Python Code — Polling Method
Write a Python program that **continuously polls** the receiver signal pin in a loop and prints the beam status:
- If the beam is broken → print `"Beam Broken"`
- If the beam is not broken → print `"Beam Not Broken"`

**Polling** means the program repeatedly checks the state of the pin at regular intervals (e.g., every 100ms). This is simple to implement but keeps the CPU occupied checking the pin even when nothing has changed.

---
### 3. Python Code — Interrupt Method (Optional)
As an alternative to polling, try implementing the same functionality using **GPIO interrupts**.

An interrupt triggers a callback function automatically whenever the signal pin changes state (rising or falling edge), rather than checking it repeatedly in a loop.
