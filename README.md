# RoboticsEducation Program

A robotics-based educational platform designed to teach programming, mathematics, and control concepts through interaction with a real robotic system.

---
## Notes on Availability & Collaboration

The full implementation of this project is currently not fully exposed in this repository.

The system is still under active development and includes additional scripts, experiments, and hardware integrations that are not yet organized for public release.

However, the architecture and capabilities presented here reflect the actual working system.

I am open to sharing more details, discussing the design, or walking through the implementation in a technical conversation.

---
## Overview

The RoboticsEducation Program is built around a physical robotic platform (myCobot 280) and integrates Python-based control, external hardware, and sensor feedback.

The goal is to transform abstract concepts into tangible experiences by allowing users to interact directly with a robot, observe behavior, and build control logic in real time.

---

## System Setup & Optimization

The robotic platform was optimized at the system level to ensure stable and efficient operation.

- Replaced original storage with an SSD for improved performance  
- Removed the default operating system  
- Deployed a minimal, headless environment (no GUI)  
- Reduced CPU and memory usage for real-time tasks  
- Remote access via SSH with VS Code Remote integration  
- Plug-and-play workflow for development and control  

This setup ensures that system resources are focused on robotics, control, and computation rather than overhead.

---
## Part A — Project Overview

This project is a robotics-based educational system designed to teach programming, mathematics, and basic robotics concepts through direct interaction with a robotic arm.

The system is built around a myCobot 280 robotic platform, controlled via Python, and integrated with external hardware components such as sensors and microcontrollers (Arduino). The goal is to create a learning environment where abstract concepts can be explored through physical execution.

### Objectives

- Provide a hands-on framework for learning Python programming  
- Introduce spatial reasoning concepts such as coordinates, transformations, and motion in 3D space  
- Bridge the gap between software and hardware by allowing students to control a real robotic system  
- Enable structured experimentation with robot movement, sensor feedback, and control logic  

### System Concept

The system follows a modular architecture where:

- High-level logic is implemented in Python  
- The robotic arm executes motion commands based on computed targets  
- External devices (e.g., Arduino-based sensors) provide input to the system  
- Communication between components is handled via serial and TCP interfaces  

This creates a closed loop of:
**input → processing → physical execution → feedback**

### Scope

The project is currently focused on building the core infrastructure required to:

- Control robot motion safely and reliably  
- Interface with external hardware components  
- Develop reusable utilities for communication and data handling  

Future development may include structured learning modules, task-based exercises, and higher-level abstractions for educational use.

---
## Part B — Robot Control Layer

The `robot/` folder contains the core classes responsible for robot initialization, motion correction, and safety enforcement.

### Available Scripts

- `robot/session.py`  
  Provides a simple entry point for starting a robot session.  
  It builds the robot object, loads calibration data if available, applies safety limits, and returns a ready-to-use robot handle.

- `robot/cobot_correction.py`  
  Implements motion correction for the myCobot robot.  
  This module handles calibration, pose estimation, error compensation, backlash correction, and corrected movement execution.

- `robot/robot_safety.py`  
  Adds a safety layer on top of the corrected robot controller.  
  It enforces workspace limits, table clearance, speed caps, and segmented motion for large moves.

### Role of the Folder

Together, these scripts create a structured robot stack:

**session setup → corrected motion → safety enforcement**

This separation allows the system to keep robot initialization, motion accuracy, and operational safety as distinct responsibilities.

---
## Part C — Hardware Interface (Arduino)

This part of the system provides the interface between Python and Arduino-based hardware components.

Its main purpose is to support:
- deployment of Arduino sketches from Python
- serial communication with external sensors and devices

---

### Available Scripts

- `arduino_tools.py`  
  Core utility for Arduino integration.  
  It wraps `arduino-cli` and provides functions for compiling sketches, uploading them to a connected board, checking board support, and detecting the serial port.  
  This module is the main deployment layer for Arduino-based components.

- `flush_and_run_ino.py`  
  A small helper script that uses `arduino_tools.py` to compile and upload a selected sketch to the Arduino.  
  It serves as a direct execution example for development and testing.

- `read_ultra.py`  
  A lightweight serial listener for reading real-time data from the Arduino.  
  It receives streamed messages over USB, parses distance-related output, and prints the values in a simple format for further use.

---

### Role in the System

The Arduino side extends the project beyond robot motion by enabling communication with external hardware.

In practice, this layer supports a simple pipeline of:

**Python deployment tools → Arduino sketch execution → sensor data streaming back to Python**

---


## Teaser

![cobot](assets/teaser.png)
