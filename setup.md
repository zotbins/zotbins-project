# Raspberry Pi 4 & LED GPIO Output Lab
## Overview

The Raspberry Pi 4 is a single-board computer with a set of **General Purpose Input/Output (GPIO)** pins that can be programmed to control external components. In this tutorial, you will set up your Raspberry Pi 4 and write a Python program to blink an LED

![RPi Diagram](https://github.com/zotbins/zotbins-project/blob/main/images/RPi1.jpg)

---
## Part 1: Raspberry Pi 4 Setup

For a full walkthrough on setting up your Raspberry Pi 4 (installing Raspberry Pi OS, configuring Wi-Fi, enabling SSH, etc.), follow the tutorial linked below:

> **Setup Tutorial:** *(https://www.youtube.com/watch?v=BpJCAafw2qE)*

Once your Pi is set up and you can access a terminal (either directly or via SSH), you are ready to proceed.

---
## Part 2: LED Circuit

### Components Needed

| Component | Quantity |
|-----------|----------|
| Raspberry Pi 4 | 1 |
| LED (any color) | 1 |
| 330Ω Resistor | 1 |
| Breadboard | 1 |
| Jumper Wires | 2 |

### GPIO Pin Descriptions

The Raspberry Pi 4 has 40 GPIO pins. For this lab, you will use the following:

| Pin | Label | Description |
|-----|-------|-------------|
| Any GPIO pin (e.g. GPIO 17) | Output | Controls the LED. Drives HIGH (3.3V) to turn on, LOW (0V) to turn off |
| GND | Ground | Reference ground for the circuit |


![RPi GPIO Diagram](https://github.com/zotbins/zotbins-project/blob/main/images/RPi2.png)


> **Note:** Always use a current-limiting resistor in series with the LED to prevent damaging the GPIO pin. A **330Ω resistor** is recommended for a standard LED with a 3.3V supply.

### Circuit Setup
1. Connect the **anode (longer leg)** of the LED to one end of the **330Ω resistor**.
2. Connect the other end of the resistor to a **GPIO output pin** (e.g. GPIO 17) on the Raspberry Pi.
3. Connect the **cathode (shorter leg)** of the LED to a **GND pin** on the Raspberry Pi.

*(LED circuit diagram goes here)*

---

## Part 3: Python Code 
Write a Python program using the **`gpiozero`** library (pre-installed on Raspberry Pi OS) to blink the LED on and off at a regular interval.

Your program should:

- Initialize the GPIO pin connected to the LED as an output.
- Continuously toggle the LED on and off with a short delay between each state (e.g. 1 second on, 1 second off).
- Run until manually stopped with `Ctrl+C`.

The `gpiozero` library provides a `LED` class that makes this straightforward:

```python
from gpiozero import LED
from signal import pause

led = LED(17)  # Replace 17 with your GPIO pin number

led.blink()    # Blinks on and off every 1 second by default
pause()        # Keeps the program running until Ctrl+C
```

---

When the program runs correctly, the LED should visibly blink on and off at a steady interval. 