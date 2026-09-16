# Simple IoT Environmental Monitoring System

A simple IoT environmental monitoring system built using a **Robo ESP32**. The system measures temperature, humidity, and analog sensor values, displays the environmental status using the **onboard NeoPixel RGB LED**, activates the **onboard buzzer** for critical conditions, and sends sensor data to **ThingSpeak** through Wi-Fi.

## Features

* 🌡️ Temperature measurement using DHT11
* 💧 Humidity measurement using DHT11
* 📊 Analog sensor reading
* 📡 Wi-Fi connectivity
* ☁️ Data logging to ThingSpeak
* 💡 Environmental status indication using the **onboard NeoPixel RGB LED**
* 🔔 Critical-condition alert using the **onboard buzzer**

## Hardware

* Robo ESP32

  * Onboard NeoPixel RGB LED
  * Onboard buzzer
* DHT11 temperature and humidity sensor
* Analog sensor
* Jumper wires

> **Note:** The buzzer and NeoPixel RGB LED are already built into the Robo ESP32 board, so no separate buzzer or RGB LED is required.

## Software

* Arduino IDE
* C/C++
* DHT_Async library
* Adafruit NeoPixel library
* ThingSpeak library
* Wi-Fi

## Pin Configuration

| Component            | Robo ESP32 Pin |
| -------------------- | -------------: |
| DHT11                |        GPIO 25 |
| Analog Sensor        |        GPIO 33 |
| Onboard Buzzer       |        GPIO 23 |
| Onboard NeoPixel RGB |        GPIO 15 |

## How the System Works

### 1. Temperature and Humidity Measurement

The DHT11 sensor is connected to **GPIO 25**.

The program uses the `DHT_Async` library to measure temperature and humidity.

```cpp
DHT_Async dht_sensor(DHT_SENSOR_PIN, DHT_SENSOR_TYPE);
```

The sensor is read approximately every **4 seconds**.

### 2. Analog Sensor Reading

An analog sensor is connected to **GPIO 33**.

The ESP32 reads the analog value using:

```cpp
an = analogRead(33);
```

### 3. Environmental Condition Detection

The program checks the temperature and humidity values using the `checkCondition()` function.

#### Critical Condition

The system enters a critical condition when:

```text
Temperature > 30°C
OR
Humidity < 20%
OR
Humidity > 80%
```

The **onboard NeoPixel RGB LED** changes to red and the **onboard buzzer** is activated.

#### Normal Condition

The system is considered normal when:

```text
Temperature: 23°C – 26°C
Humidity: 40% – 60%
```

The onboard NeoPixel RGB LED changes to green.

#### Warning Condition

The system enters a warning condition when the values fall outside the normal range but do not reach the critical conditions.

The onboard NeoPixel RGB LED changes to yellow.

### 4. Onboard RGB LED

The Robo ESP32's built-in NeoPixel RGB LED provides a visual indication of the environmental condition.

| Condition | LED       |
| --------- | --------- |
| Normal    | 🟢 Green  |
| Warning   | 🟡 Yellow |
| Critical  | 🔴 Red    |

The NeoPixel is controlled through **GPIO 15**.

### 5. Onboard Buzzer

The Robo ESP32 has a built-in buzzer connected to **GPIO 23**.

When a critical condition is detected, the program generates a 500 Hz tone:

```cpp
tone(23, 500);
```

The buzzer is turned on and off repeatedly to provide an audible warning.

### 6. ThingSpeak Data Logging

The ESP32 connects to Wi-Fi and sends the sensor readings to ThingSpeak.

The data is assigned to three ThingSpeak fields:

```cpp
ThingSpeak.setField(1, temperature);
ThingSpeak.setField(2, humidity);
ThingSpeak.setField(3, an);
```

| ThingSpeak Field | Data          |
| ---------------- | ------------- |
| Field 1          | Temperature   |
| Field 2          | Humidity      |
| Field 3          | Analog Sensor |

The data is uploaded approximately every **20 seconds**.

## Data Flow

```text
       DHT11 ──────────┐
                       │
  Analog Sensor ───────┤
                       ↓
                 Robo ESP32
                  /       \
                 ↓         ↓
        Onboard RGB LED   Onboard Buzzer
                 │
                 ↓
                Wi-Fi
                 │
                 ↓
             ThingSpeak
                 │
                 ↓
      Temperature / Humidity /
          Analog Data
```

## Project Structure

```text
├── README.md
├── environmental_monitoring.ino
├── circuit_diagram.png
├── components.md
└── thingspeak_output.png
```

## Future Improvements

* Add more environmental sensors
* Improve the condition thresholds
* Add automatic notifications
* Create a web or mobile dashboard
* Analyse historical sensor data
* Add air-quality monitoring
* Improve power efficiency

## Author

**Ahmad Nijad**
