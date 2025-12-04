🚗 Vehicle Fault Detection & Logging System (VFDLS)

This project is the final requirement for my Embedded Systems course at Edges For Training.
The goal was to build a small automotive-style diagnostic system using two ATmega32 microcontrollers working together in a dual-ECU architecture.

The system monitors several basic vehicle-related signals, detects abnormal conditions, and stores fault codes in external EEPROM so they remain available even after a reset.
All interaction with the system is done through an LCD and keypad connected to the HMI ECU.

🔧 System Overview

The project is built around two ATmega32 MCUs running at 8 MHz:

1. HMI ECU

Handles everything the user interacts with:

4×16 LCD

4×4 keypad

UART communication with the Control ECU

Menu navigation, live data request, fault retrieval, start/stop commands

2. Control ECU

Responsible for:

Reading sensors (LM35 for temperature, ultrasonic for distance)

Controlling DC motors (car window simulation)

Detecting fault conditions

Logging Diagnostic Trouble Codes (DTCs) to a 24C16 external EEPROM via I2C

Sending live data back to the HMI ECU over UART

📡 Monitored Subsystems
Engine Temperature (LM35 → ADC)

Normal measurement of engine temperature

Logs fault if temperature > 90°C

DTC: P002 – ENGINE_HIGH_TEMPERATURE

Ultrasonic Sensor (Parking Aid)

Measures distance between the car and obstacles

Logs fault if distance < 10 cm

DTC: P001 – ACCIDENT_MIGHT_HAPPENED

Car Windows (DC Motors)

Two motors representing two windows

Each window has open/close pushbuttons

States displayed on the HMI LCD

💾 Fault Logging

All faults are saved into external EEPROM (24C16) using I2C.
Logged codes stay saved even after powering off.

The HMI ECU can retrieve:

All stored fault codes

A scrolling list of DTCs on the LCD

🖥️ User Interface (HMI)

Main menu includes:

Start Operation

Display Live Values

Retrieve Stored Faults

Stop Monitoring

Live display shows:

Temp: XX°C
Distance: XX cm
Win1: Open/Closed   Win2: Open/Closed

📚 Technologies & Drivers Used

UART for ECU-to-ECU communication

I2C (TWI) for EEPROM

ADC for LM35

PWM for DC motors

ICU for ultrasonic sensor

Timers (Timer1 Compare Mode on HMI ECU)

LCD & Keypad drivers

Layered architecture

🛠️ Tools Used

Eclipse IDE (two projects in one workspace)

Proteus simulation

AVR-GCC toolchain

🎯 Project Purpose

The aim of this project was to bring together everything learned throughout the course—drivers, communication protocols, layering, and working with real peripherals—into one system that behaves like a simplified automotive ECU network.
