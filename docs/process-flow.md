# Process Flow Notes

## Project Structure

The project was developed using modular Siemens PLC logic. The two station-level functions included in this repository are:

* `Processing Station [FC5]`
* `Sorting Station [FC6]`

These function blocks were called by a main/top-level control block that handled overall system integration and the specific PLC addresses used in the university setup.

## Processing Station Function

The processing station function controls the workpiece from initial detection through processing and transfer to the sorting station.

### Main Actions

1. Start homing sequence
2. Move linear robot to safe/home position
3. Reset gripper and check gripper safety
4. Check oven status
5. Set turntable to required position
6. Check processing conveyor
7. Wait for workpiece detection
8. Move robot to the oven position
9. Pick up the workpiece
10. Move workpiece to turntable
11. Drop workpiece on turntable
12. Rotate turntable to saw position
13. Start and stop saw process using timers
14. Move workpiece to oven
15. Load workpiece into oven
16. Start baking/light sequence
17. Open oven and unload workpiece
18. Move workpiece to processing conveyor
19. Push workpiece to conveyor
20. Move workpiece to sorting station

## Sorting Station Function

The sorting station function receives the workpiece, detects its colour and ejects it into the correct slider.

### Main Actions

1. Reset all ejectors during homing
2. Check whether all homing conditions are satisfied
3. Indicate homed state
4. Stop the processing conveyor after the workpiece reaches the sorting station
5. Read the analogue colour sensor voltage
6. Store the minimum voltage value
7. Determine colour using threshold ranges
8. Sort white, red and blue objects into different sliders
9. Use encoder values to time the ejector position
10. Reject item if it does not meet expected sorting conditions
11. Reset and wait for the next workpiece

## Colour Detection Concept

The sorting station uses the colour sensor voltage to classify the workpiece.

The PLC logic stores a minimum voltage value and compares it with ranges to determine the object colour.

Example logic concept:

| Colour | Voltage Range Used in Logic                                                  |
| ------ | ---------------------------------------------------------------------------- |
| White  | 6.0 to 6.8                                                                   |
| Red    | 7.0 to 7.9                                                                   |
| Blue   | 8.0 to 8.7                                                                   |
| Reject | Used when sorting condition is not valid or slider handling limit is reached |

## Sorting Mechanism

The sorting station uses:

* Sorting conveyor motor
* Light barrier sensors
* Encoder counter value
* Pneumatic ejectors
* Slider A, Slider B and Slider C
* Compressor control
* Timers for ejector activation and reset

## Troubleshooting Notes

* Sensor values changed slightly during testing depending on object position and lighting.
* Timing delays were important for robot movement, gripper operation, saw timing, oven sequence and ejector triggering.
* The colour sensor threshold values had to be adjusted based on real readings.
* The sorting station required encoder-based positioning so the ejector activated at the correct point.
* Stop and reset logic was included to safely deactivate motors, compressor and actuators.

## Skills Demonstrated

* Siemens PLC ladder logic
* Modular function design
* Sequential automation control
* Homing and safety-state handling
* Analogue sensor thresholding
* Timer-based actuator control
* Conveyor and robot coordination
* Industrial troubleshooting and documentation
