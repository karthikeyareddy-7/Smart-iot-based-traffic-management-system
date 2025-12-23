

# ESP32 Smart Traffic Light Control System

## Overview

This project is a **smart traffic light control system** implemented using an **ESP32 microcontroller**. The system dynamically manages traffic signals at a 4-way intersection based on real-time traffic density measured by **IR/analog sensors**. It automates traffic flow to reduce congestion, improve safety, and optimize signal timings.

---

## Project Workflow

The system consists of the following components and workflow:

### 1. Hardware Components

* **ESP32 Development Board** – microcontroller for processing and controlling traffic lights.
* **IR/Analog Traffic Sensors** – four sensors to measure vehicle density for each direction:

  * `SENSOR_NORTH` – Pin 32
  * `SENSOR_SOUTH` – Pin 34
  * `SENSOR_EAST` – Pin 35
  * `SENSOR_WEST` – Pin 15
* **LEDs for Traffic Signals**:

  * Red, Yellow, Green LEDs for each direction
  * Pins assigned for each light (e.g., `RED_NORTH` – Pin 5, `GREEN_WEST` – Pin 19, etc.)

---

### 2. Traffic Light Logic

* Traffic lights have **three states**:

  * `RED` – Stop
  * `YELLOW` – Prepare to stop
  * `GREEN` – Go
* **Timing Constants**:

  * Green: 10 seconds (`GREEN_TIME`)
  * Yellow: 2 seconds (`YELLOW_TIME`)
* **Traffic Density Thresholds**:

  * `MIN_SENSOR_THRESHOLD` = 50
  * `MAX_SENSOR_THRESHOLD` = 200
* Traffic density is calculated from sensor readings and mapped to a percentage (0–100).

---

### 3. System Setup

* Each sensor pin is configured as `INPUT`.
* LED pins are configured as `OUTPUT`.
* ESP32 serial monitor is initialized for debugging and traffic monitoring.

```cpp
pinMode(SENSOR_NORTH, INPUT);
pinMode(RED_NORTH, OUTPUT);
// … repeat for all sensors and LEDs
Serial.begin(9600);
```

---

### 4. Main Program Workflow (`loop()`)

1. **Read sensors** for all four directions.
2. **Calculate traffic density** using `calculateDensity()` function.
3. **Update traffic signals** for each direction based on:

   * Current traffic density
   * State of other traffic directions
   * Signal timing logic
4. **Print status** of all traffic lights and sensor readings to the serial monitor.
5. Delay 1 second before next iteration.

---

### 5. Functions

* `readSensor(int sensorPin)` – Reads the analog value from the sensor and handles invalid readings.
* `calculateDensity(int sensorValue)` – Maps sensor readings to a 0–100 traffic density scale.
* `updateTrafficSignal(int redPin, int yellowPin, int greenPin, int* state, int density, int otherState1, int otherState2, int otherState3)` – Updates the traffic light state based on density, timing, and other signals.
* `printTrafficLightStatus(String direction, int state, unsigned long greenTime, unsigned long yellowTime)` – Prints current light status and remaining time to the serial monitor.

---

### 6. Features

* **Dynamic Traffic Control**: Adjusts green light durations based on real-time traffic density.
* **Simultaneous State Awareness**: Ensures safety by checking other directions before changing signals.
* **Debugging Support**: Serial output for monitoring sensor values and light states.
* **Configurable Timings and Thresholds**: Easily adjustable constants for green/yellow duration and sensor thresholds.

---

### 7. Hardware Connections

| Direction | Sensor Pin | Red LED Pin | Yellow LED Pin | Green LED Pin |
| --------- | ---------- | ----------- | -------------- | ------------- |
| North     | 32         | 5           | 4              | 2             |
| South     | 34         | 33          | 25             | 26            |
| East      | 35         | 27          | 14             | 12            |
| West      | 15         | 22          | 21             | 19            |

---

### 8. How to Use

1. Connect ESP32 to your computer.
2. Connect LEDs and sensors as per the pin configuration table.
3. Open the Arduino IDE and select the ESP32 board.
4. Upload the code to the ESP32.
5. Open the Serial Monitor at 9600 baud to observe traffic light status and sensor readings.
6. Observe the traffic lights change dynamically according to simulated traffic density.

---

### 9. Future Enhancements

* Integrate **Wi-Fi/IoT capabilities** for remote monitoring.
* Use **camera or IR detection** for more accurate traffic density measurement.
* Implement **adaptive green light duration** using historical traffic data.
* Add **pedestrian signals** and countdown timers.
* Integrate with **cloud dashboards** for smart city applications.

---

### 10. Summary

This ESP32-based smart traffic light system demonstrates how **real-time sensor data** can be used to optimize traffic management at intersections. It provides a foundation for more advanced IoT and smart city traffic solutions.

---

