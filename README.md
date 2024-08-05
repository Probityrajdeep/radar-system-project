# Radar System Project

![Radar System](https://via.placeholder.com/800x200.png?text=Radar+System+Project)

## Overview

This project demonstrates a radar system using an ESP32 and ultrasonic sensor. The radar data is displayed on a web interface hosted on the ESP32.

## Features

- **Real-Time Radar Display**: Shows the radar data in real-time.
- **Control Servo Motors**: Adjust the radar angle using buttons or keyboard.
- **Responsive Design**: Works on both desktop and mobile devices.

## Hardware Required

- ESP32
- Ultrasonic Sensor
- Servo Motor
- Breadboard
- Jumper Wires

## Getting Started

### Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/Probityrajdeep/radar-system-project.git
    ```
2. **Navigate to the project directory**:
    ```bash
    cd radar-system-project
    ```

### Usage

1. **Upload the code to ESP32**:
    - Connect your ESP32 to your computer.
    - Open the project in Arduino IDE.
    - Select the correct board and port.
    - Upload the code.

2. **Connect the hardware**:
    - Follow the wiring diagram provided in the project.

3. **Open the web interface**:
    - Connect to the ESP32's Wi-Fi network.
    - Open a browser and navigate to `http://192.168.4.1`.

### How to do :
Components Needed:
ESP32
Ultrasonic Sensor (HC-SR04)
Servo Motor
Jumper Wires
Breadboard (optional)
Wiring Diagram:
Ultrasonic Sensor:
VCC to VV (3.3V on ESP32)
TRIG to D5 on ESP32
ECHO to D18 on ESP32
GND to GND on ESP32
Servo Motor:
Signal Wire to D4 on ESP32
Positive Wire to VIN (5V on ESP32)
Ground Wire to GND on ESP32
Step-by-Step Instructions:
Connect the Ultrasonic Sensor:

Connect the VCC pin of the ultrasonic sensor to the 3.3V (VV) pin of the ESP32.
Connect the TRIG pin of the ultrasonic sensor to GPIO 5 (D5) on the ESP32.
Connect the ECHO pin of the ultrasonic sensor to GPIO 18 (D18) on the ESP32.
Connect the GND pin of the ultrasonic sensor to the GND pin on the ESP32.
Connect the Servo Motor:

Connect the signal wire of the servo motor to GPIO 4 (D4) on the ESP32.
Connect the positive wire of the servo motor to the VIN (5V) pin on the ESP32.
Connect the ground wire of the servo motor to the GND pin on the ESP32.
Power the ESP32:

You can power the ESP32 via USB from your computer or an external power supply.
Visual Diagram:

Notes:
Ensure all connections are secure and double-check the pin assignments.
Use a breadboard if you want a more stable setup for testing.
This setup will allow you to control the servo motor and read data from the ultrasonic sensor using the ESP32. You can use this configuration to create a simple radar system that displays data on a web interface hosted by the ESP32.



License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgments
Inspiration and support from the open-source community.
Special thanks to all contributors.
