# IoT-Based-Solar-Monitoring-System


## 📌 Overview
This project implements an IoT-enabled solar monitoring system to track the real-time performance of a rooftop or utility-scale solar PV installation. It includes sensor integration for voltage, current, temperature, and irradiance, data transmission via MQTT, and dashboard visualization using a web interface.

---

## 🏠 Hardware & Assumptions
```python
# Solar Monitoring Parameters
voltage = 0          # Placeholder for real-time voltage data
current = 0          # Placeholder for real-time current data
temperature = 0      # Panel surface temperature
irradiance = 0       # Solar irradiance in W/m2

# IoT Communication Setup
mqtt_broker = "broker.hivemq.com"
topic = "solar/monitor"
```

---

## 🧼 Sensor Integration & Data Transmission (ESP32 / Raspberry Pi)
```python
import time
import random
import paho.mqtt.client as mqtt
import json

client = mqtt.Client()
client.connect(mqtt_broker, 1883, 60)

while True:
    # Simulate sensor readings
    voltage = round(random.uniform(320, 360), 2)
    current = round(random.uniform(2, 5), 2)
    temperature = round(random.uniform(30, 45), 2)
    irradiance = round(random.uniform(600, 1000), 2)

    payload = json.dumps({
        "voltage": voltage,
        "current": current,
        "power": round(voltage * current, 2),
        "temperature": temperature,
        "irradiance": irradiance
    })

    client.publish(topic, payload)
    print("Published:", payload)
    time.sleep(5)
```

---

## 📊 Real-Time Dashboard (Flask + Chart.js)
```python
# This part serves as a placeholder backend for a real-time dashboard using Flask
from flask import Flask, jsonify, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/data')
def get_data():
    return jsonify({
        "voltage": voltage,
        "current": current,
        "power": round(voltage * current, 2),
        "temperature": temperature,
        "irradiance": irradiance
    })

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 📄 Deliverables
- Live solar monitoring using IoT
- MQTT-based real-time data transfer
- Flask dashboard with live updates
- Sensor integration code for ESP32/Raspberry Pi

---

## ✅ Tools Used
- ESP32 or Raspberry Pi
- Python (Flask, Paho MQTT, JSON)
- MQTT Broker (HiveMQ or Mosquitto)
- Sensors: Voltage/Current sensor, DHT11/DHT22, Irradiance sensor (LDR or pyranometer)
- Web technologies (HTML, Chart.js)
