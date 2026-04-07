# Arduino Elevator System

This project is a functional miniature elevator control system built with an **Arduino Uno** and an **L298N Motor Driver**. It uses a time-based, open-loop control logic to navigate between floors, featuring custom gravity-compensation to handle the physical weight of the elevator cabinet.

## 🚀 Features

* **Asymmetrical Timing Control:** Accounts for gravity by using precise, measured milliseconds for travel times (moving up requires more time/power than moving down).
* **Open-Loop Floor Targeting:** Navigates 3 simulated floors (Up 1, Up 2, Down 1, Down 2) without the need for complex external limit switches.
* **Hardware Simplification:** Utilizes the Arduino's internal pull-up resistors (`INPUT_PULLUP`) to eliminate the need for physical resistors on the button circuits.
* **Input Debouncing & Safety:** Includes a `waitForRelease` function to prevent double-triggering or continuous looping if a user holds a button down.
* **Split Power Architecture:** Logic is powered by the Arduino, while the heavy motor load is powered via the L298N driver using an external power source to prevent voltage drops.

## 🛠️ Hardware Required

* 1x Arduino Uno
* 1x L298N Motor Driver Module
* 1x DC Motor (Elevator Winch/Hoist)
* 4x Push Buttons
* 1x External Battery (e.g., 9V or 4x AA Battery pack) for the motor
* Jumper Wires

## 🔌 Pin Mapping / Wiring Guide

| Component | Pin / Terminal | Arduino Pin / Connection | Notes |
| :--- | :--- | :--- | :--- |
| **L298N Driver** | ENA | `Pin 5` | Controls motor speed (PWM) |
| **L298N Driver** | IN1 | `Pin 4` | Controls direction |
| **L298N Driver** | IN2 | `Pin 3` | Controls direction |
| **Button: Up 1** | Leg 1 | `Pin 8` | Leg 2 connects to `GND` |
| **Button: Up 2** | Leg 1 | `Pin 9` | Leg 2 connects to `GND` |
| **Button: Down 1**| Leg 1 | `Pin 10` | Leg 2 connects to `GND` |
| **Button: Down 2**| Leg 1 | `Pin 11` | Leg 2 connects to `GND` |

*(Note: The L298N requires a common ground with the Arduino to share logic signals).*

## ⚙️ How It Works (The Engineering)

The system operates on an **Event-Driven Sequence**. When a user presses a button, the Arduino reads the `LOW` signal and executes a precise block of code:
1. **Engage Motor:** The L298N H-Bridge is triggered to send power to the motor in the correct polarity (Up or Down).
2. **Precision Delay:** The system waits for a highly specific amount of time based on real-world calibration (e.g., `3025ms` for Up 1 Floor, but only `2082ms` for Down 1 Floor due to gravity assistance).
3. **Brake:** Power is cut to the motor.
4. **Lockout:** The code pauses until the user physically releases the button, preventing accidental repeat movements.

## 💻 Installation and Setup

1. Assemble the hardware according to the Pin Mapping table above.
2. Clone this repository or download the `.ino` file.
3. Open the file in the **Arduino IDE**.
4. Connect your Arduino Uno to your computer via USB.
5. Select your COM port and Arduino Uno board in the IDE.
6. Click **Upload**.

---
## 🤝 Collaboration & Acknowledgments

This project was developed as a collaborative engineering effort. 
Adam Tamer Ghobashy - @Adam-Ghobashy
Mai Ahmed Khalaf - @MaiKhalaf
Basma Ahmed
Hazem Mohamed
