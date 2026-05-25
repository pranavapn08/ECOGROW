# 🌱 EcoGrow — Smart Plant Monitoring System

EcoGrow is an IoT-based smart plant monitoring system built with ESP8266 that monitors soil moisture, water level, and temperature in real time using the Blynk app.

---

## 📱 Features

- 🌍 **Soil Moisture Monitoring** — Detects if the soil is wet or dry
- 💧 **Water Level Monitoring** — Measures available water in the tank
- 🌡️ **Temperature Monitoring** — Reads surrounding temperature using DS18B20 sensor
- ⚙️ **Remote Motor Control** — Turn the water pump ON/OFF from your phone via Blynk app
- 📲 **Real-time Updates** — Sensor data sent to Blynk app every 2 seconds over WiFi

---

## 🛠️ Hardware Components

| Component | Description |
|---|---|
| ESP8266 | WiFi microcontroller (NodeMCU) |
| Soil Moisture Sensor | Digital output (DO) sensor |
| Water Level Sensor | Analog output (AO) sensor |
| DS18B20 Temperature Sensor | OneWire digital temperature sensor |
| Relay Module | Controls the water pump/motor |
| Water Pump/Motor | For automated irrigation |

---

## 📌 Pin Configuration

| Sensor/Component | ESP8266 Pin |
|---|---|
| Soil Moisture Sensor (DO) | D5 |
| Water Level Sensor (AO) | A0 |
| Temperature Sensor | D8 |
| Relay (Motor Control) | D6 |

---

## 📲 Blynk Virtual Pins

| Virtual Pin | Function |
|---|---|
| V0 | Soil Moisture |
| V1 | Water Level |
| V2 | Temperature |
| V3 | Relay (Motor ON/OFF) |

---

## 🚀 Getting Started

### 1. Install Required Libraries
In Arduino IDE, install the following libraries via **Library Manager**:
- `Blynk` by Volodymyr Shymanskyy
- `OneWire` by Paul Stoffregen
- `DallasTemperature` by Miles Burton

### 2. Set Up Blynk
- Create an account at [blynk.cloud](https://blynk.cloud)
- Create a new template named **EcoGrow**
- Add datastream virtual pins V0–V3
- Get your **Auth Token**

### 3. Configure the Code
Open `Blynk_app.ino` and update these values:
```cpp
#define BLYNK_AUTH_TOKEN "your_auth_token_here"
char ssid[] = "your_wifi_name";
char pass[] = "your_wifi_password";
```

### 4. Upload to ESP8266
- Select **NodeMCU 1.0** as the board in Arduino IDE
- Connect your ESP8266 via USB
- Click **Upload**

---

## 📂 Project Structure

```
EcoGrow/
├── Blynk_app.ino       # Main Arduino code
├── README.md           # Project documentation
└── images/             # Project photos
```

---

## 🔮 Future Implementation

### 📷 Smart Camera Integration (Plant Pot CCTV)
- Add a small camera module (such as ESP32-CAM) to the plant pot
- The camera will act as a **dual-purpose CCTV** — monitoring both the plant and its surroundings for security
- Live camera feed accessible remotely through the Blynk app or a web dashboard
- Motion detection alerts sent to the user's phone when movement is detected near the plant

### 🤖 AI-Powered Plant Care Assistant
- Integrate a computer vision AI model to **analyze plant health** from camera images
- Automatically detect common plant problems such as:
  - 🍂 Yellowing or wilting leaves
  - 🍄 Fungal infections or mold
  - 🐛 Pest infestations
- AI will send **personalized care suggestions** to the user such as:
  - *"Your plant looks overwatered, reduce irrigation frequency"*
  - *"Leaves show signs of nutrient deficiency, consider fertilizing"*
  - *"Possible pest detected, inspect the plant closely"*

### 🌦️ Weather-Based Automation
- Fetch local weather data via API and automatically adjust watering schedules based on rainfall predictions

### 📈 Data Logging & Analytics
- Store historical sensor data and display graphs showing plant health trends over time

---

## ⚠️ Security Note

Never upload your real WiFi credentials or Blynk Auth Token to GitHub. Use placeholder values in the code before pushing.

---

## 👨‍💻 Author

Made with ❤️ as part of an IoT project.
