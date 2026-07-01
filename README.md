# Miniature Industrial Automation and Sorting System

## Overview

This project is a miniature industrial automation system developed as part of my Industrial Automation coursework. The system represents a small-scale automated industrial process where a workpiece is moved through processing and sorting stations using Siemens PLC logic, sensors, conveyors, a linear robot, a turntable, an oven, a saw, pneumatic actuators and ejector mechanisms.

The project was structured using modular PLC function blocks. The processing station logic and sorting station logic were written as separate functions and called by the main/top-level control block, which handled overall system integration and university PLC-specific addressing.

## Project Evidence

| File                              | Description                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------- |
| `docs/processing-station-fc5.pdf` | Siemens TIA Portal LAD logic export for the processing station function block |
| `docs/sorting-station-fc6.pdf`    | Siemens TIA Portal LAD logic export for the sorting station function block    |
| `docs/process-flow.md`            | Simplified explanation of the process sequence and control logic              |

## System Modules

### Processing Station

The processing station controls the sequence from workpiece detection to processing and transfer. It includes:

* Homing sequence
* Linear robot movement
* Gripper lowering and gripping
* Turntable positioning
* Saw operation
* Oven loading and baking sequence
* Conveyor transfer to the sorting station
* Stop and reset handling

### Sorting Station

The sorting station receives the processed workpiece and sorts it based on colour sensor readings. It includes:

* Homing and ejector reset
* Sorting conveyor control
* Colour voltage detection
* White, red and blue object classification
* Reject condition handling
* Encoder-based position tracking
* Ejector control for different sliders
* Automatic reset for the next workpiece

## Tools and Technologies

* Siemens PLC
* TIA Portal
* Ladder logic
* Function blocks
* Analogue colour sensor
* Light barrier sensors
* Linear robot
* Turntable
* Conveyor system
* Oven and saw simulation modules
* Pneumatic gripper and ejectors

## Working Logic

1. The operator starts the system using the automatic mode controls.
2. The system performs homing to bring the robot, gripper, turntable, oven and conveyors into safe starting positions.
3. A workpiece is detected at the processing station.
4. The linear robot picks the workpiece and places it on the turntable.
5. The turntable moves the workpiece to the saw station.
6. The saw process is triggered for the required duration.
7. The workpiece is moved to the oven station.
8. The oven door and feeder sequence load the workpiece into the oven.
9. After the baking sequence, the workpiece is transferred to the processing conveyor.
10. The conveyor moves the workpiece to the sorting station.
11. The sorting station reads the colour sensor voltage and determines the object colour.
12. Based on the detected colour, the system activates the correct ejector/slider.
13. The system resets and waits for the next workpiece.

## Colour Detection Logic

The sorting station uses an analogue colour sensor. The PLC stores the minimum detected voltage value and compares it with threshold ranges to classify the workpiece.

Example threshold concept used in the logic:

| Colour | Voltage Range Concept                                                                         |
| ------ | --------------------------------------------------------------------------------------------- |
| White  | Lower voltage range                                                                           |
| Red    | Mid voltage range                                                                             |
| Blue   | Higher voltage range                                                                          |
| Reject | Used when the item does not fit the expected valid sorting condition or slider capacity logic |

## What I Worked On

* Developed modular Siemens PLC ladder logic for processing and sorting station functions
* Created station-level automation logic that could be called by the main control function
* Programmed homing, stop, reset and automatic mode sequences
* Controlled robot movement, gripper operation, turntable movement, saw timing, oven loading and conveyor transfer
* Implemented colour sensor threshold logic for object classification
* Added ejector control for sorting workpieces into different sliders
* Used timers, set/reset logic, sensor inputs and actuator outputs to manage process sequencing
* Troubleshot real hardware issues such as sensor variation, timing delays and actuator sequencing

## Key Learning Outcomes

* PLC-based industrial automation design
* Ladder logic development in Siemens TIA Portal
* Modular function block design
* Sensor-actuator coordination
* Analogue sensor thresholding
* Sequential control logic
* Industrial process troubleshooting
* Difference between simulation logic and real hardware behaviour

## Current Status

This repository documents the processing and sorting station logic from my Industrial Automation coursework. The main top-level integration block is not included because it contains university PLC system-specific addressing and integration details. The included function blocks show the main processing and sorting station logic developed for the miniature industrial automation system.

## Future Improvements

* Add simplified flowchart of the full process
* Add state diagram for processing and sorting stations
* Add photos or screenshots of the physical setup
* Add a sensor threshold table from final testing
* Add troubleshooting notes from demo validation
* Add a short explanation of how this system could scale to a real industrial automation process
