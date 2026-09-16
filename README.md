# ESP32-Environmental-Monitoring-System

A simple IoT project using an **ESP32** to monitor environmental conditions and send sensor data to **ThingSpeak** through Wi-Fi.

## Features

* 🌡️ Measures temperature
* 💧 Measures humidity
* 📊 Reads analog sensor data
* 📡 Sends data to ThingSpeak
* 💡 Uses an RGB LED to indicate environmental conditions
* 🔔 Activates a buzzer during critical conditions

## Hardware

* ESP32
* DHT11 temperature & humidity sensor
* Analog sensor
* RGB NeoPixel
* Buzzer
* Jumper wires

## Software

* Arduino IDE
* C/C++
* ThingSpeak
* Wi-Fi

## Project Structure

```text
├── README.md
├── environmental_monitoring.ino
├── circuit_diagram.png
├── components.md
└── thingspeak_output.png
```

## How It Works

The ESP32 collects temperature, humidity, and analog sensor readings. The data is sent over Wi-Fi to ThingSpeak, where it can be monitored through graphs.

The RGB LED and buzzer provide local indications based on the measured environmental conditions.

## ThingSpeak

The sensor data is uploaded to a ThingSpeak channel for visualization and monitoring.

## Future Improvements

* Add more environmental sensors
* Improve the condition-detection system
* Add notifications for critical conditions
* Create a web or mobile dashboard
* Improve data analysis and visualization

## Author

Ahmad Nijad
