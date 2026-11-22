# 🌱 Smart Agriculture Monitoring System using ESP32

![Platform](https://img.shields.io/badge/Platform-ESP32-blue)
![Framework](https://img.shields.io/badge/Framework-Arduino-00979D)
![Language](https://img.shields.io/badge/Language-C%2B%2B%20%7C%20JavaScript-orange)
![Telegram](https://img.shields.io/badge/Alerts-Telegram%20Bot-26A5E4)
![License](https://img.shields.io/badge/License-MIT-green)

An IoT-based Smart Agriculture Monitoring System that collects real-time environmental and soil data using an ESP32 and low-cost sensors. It serves a responsive live web dashboard over Wi-Fi and sends Telegram notifications when configured alert conditions occur.

---

## 🎬 Demo Video (Output)

<!--
HOW TO ADD THE VIDEO ON GITHUB:
1. Open this README on GitHub -> click the pencil (Edit) icon.
2. Drag & drop your demo video (.mp4 / .mov, under 10 MB on free plans) into the editor.
3. GitHub uploads it and inserts a link like:
   https://github.com/user-attachments/assets/xxxxxxxx
4. Replace the placeholder link below with that link and commit.
   A bare link on its own line is shown as an inline video player.
-->

https://github.com/user-attachments/assets/27085e01-33fc-4499-b90b-df3d471a4661

> If the video is large, upload it to YouTube and use a clickable thumbnail instead:
>
> [![Watch the demo](docs/images/dashboard-main.png)](https://youtu.be/YOUR_VIDEO_ID)

---

## 📌 1. Project Overview

The system monitors temperature, humidity, soil moisture and rainfall. The ESP32 processes the readings and hosts a local web dashboard accessible from any device on the same Wi-Fi network.

It also provides automatic LED and buzzer alerts, adjustable thresholds, soil calibration and Telegram notifications.

## ✨ 2. Key Features

- Real-time temperature and humidity monitoring
- Soil moisture monitoring with percentage conversion
- Rain detection using an analog rain sensor
- Live web dashboard with dark and light themes
- Graphs of sensor history with min / avg / max / now values
- Last 60 readings stored in ESP32 RAM
- Automatic LED and buzzer alerts
- Manual ON / OFF / AUTO control modes
- Adjustable alert thresholds
- Soil moisture dry and wet calibration
- Telegram notifications for configured alerts
- Wi-Fi status and signal strength monitoring
- Settings retained after power restart (ESP32 Preferences)

## 🏗️ 3. System Architecture

```text
      DHT11 Sensor
  (Temperature & Humidity)
           |
      Soil Sensor
           |
      Rain Sensor
           |
           v
      ESP32 DevKit V1
           |
      Data Processing
           |
      Wi-Fi Connection
           |
     +-----+------+
     |            |
     v            v
 Web Dashboard  Telegram Bot
     |
     +----------------+
     |                |
     v                v
  Live Charts    Sensor Alerts
     |
     v
 LED and Buzzer
```

## 🔩 4. Hardware Requirements

| Component | Quantity | Purpose |
|---|---:|---|
| ESP32 DevKit V1 | 1 | Main controller |
| DHT11 Sensor | 1 | Temperature and humidity |
| Soil Moisture Sensor (analog) | 1 | Soil moisture measurement |
| Rain Sensor Module (analog) | 1 | Rain detection |
| LED | 1 | Visual alert |
| Buzzer | 1 | Sound alert |
| 220Ω Resistor | 1 | LED current limiting |
| 100Ω Resistor | 1 | Buzzer current limiting |
| Jumper Wires | As required | Connections |
| USB Cable / 5V Supply | 1 | Power supply |
| Breadboard | 1 | Prototyping |

## 🔌 5. Circuit Connections

| Component | Sensor Pin | ESP32 Pin |
|---|---|---|
| DHT11 | VCC | 3.3V |
| DHT11 | DATA | GPIO 27 |
| DHT11 | GND | GND |
| Soil Sensor | VCC | 3.3V |
| Soil Sensor | AO | GPIO 35 (ADC1_CH7) |
| Soil Sensor | GND | GND |
| Rain Sensor | VCC | 3.3V |
| Rain Sensor | AO | GPIO 34 (ADC1_CH6) |
| Rain Sensor | GND | GND |
| LED | Positive (via 220Ω) | GPIO 26 |
| LED | Negative | GND |
| Buzzer | Positive (via 100Ω) | GPIO 25 |
| Buzzer | Negative | GND |

**Important:**
- Power the ESP32 with 5V (VIN) from USB or an adapter.
- Use a common GND for all modules.
- Analog sensor outputs must stay within the ESP32 ADC limit (3.3V).
- Verify the buzzer's voltage/current needs; use a transistor driver if necessary.
- The wiring must match the actual assembled circuit.

### Circuit Diagram

![ESP32 Smart Agriculture Wiring Diagram](docs/images/wiring-diagram.png)

## 💻 6. Technology Stack

**Hardware:** ESP32 DevKit V1, DHT11, analog soil moisture sensor, analog rain sensor

**Embedded software:** C++, Arduino Framework, Arduino IDE

**Frontend:** HTML5, CSS3, JavaScript, HTML Canvas API

**Communication:** Wi-Fi, HTTP, JSON, Telegram Bot API

### Libraries

| Library | Purpose |
|---|---|
| `WiFi.h` | Wi-Fi connectivity |
| `WebServer.h` | Local web server |
| `Preferences.h` | Persistent settings |
| `HTTPClient.h` | HTTP communication |
| `WiFiClientSecure.h` | Secure Telegram connection |
| `DHT.h` | DHT11 sensor readings |

Install **DHT sensor library by Adafruit** from the Arduino IDE Library Manager (and **Adafruit Unified Sensor** if prompted). All other libraries come with the ESP32 Arduino core.

## ⚙️ 7. Software Requirements

1. Arduino IDE
2. ESP32 Board Package
3. DHT Sensor Library by Adafruit
4. Adafruit Unified Sensor Library
5. USB cable for programming
6. Wi-Fi network with internet access (for Telegram)

## 🚀 8. Installation and Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/TEJA-100/YOUR_REPOSITORY_NAME.git
cd YOUR_REPOSITORY_NAME
```

### Step 2: Open Arduino IDE

- Open the firmware `.ino` file.
- Select **ESP32 Dev Module** and the correct COM port.
- Install the required DHT libraries.

### Step 3: Configure Wi-Fi

```cpp
const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_WIFI_PASSWORD";
```

### Step 4: Configure Telegram

Create a bot with **@BotFather**, then set the token and your chat ID.

```cpp
const char* tgToken = "YOUR_BOT_TOKEN";
const char* tgChatId = "YOUR_CHAT_ID";
```

> ⚠️ Never commit real Wi-Fi passwords or bot tokens to GitHub. Use placeholders and revoke any token that was exposed.

### Step 5: Upload the Code

- Connect the ESP32 and click **Upload**.
- Open Serial Monitor at **115200 baud**.
- Wait for the Wi-Fi connection and note the printed IP.

### Step 6: Open the Dashboard

```text
http://ESP32_LOCAL_IP
```

## 📊 9. Dashboard Overview

A single-page monitoring interface.

**Main cards:** Air temperature (°C), air humidity (%), soil moisture (%), rainfall status

**Graphs:** Temperature, humidity and soil moisture history with min / avg / max / now

**System information:** ESP32 connection, Wi-Fi signal, uptime, last update, next reading, stored reading count

**Control panel:** LED and buzzer Auto / On / Off, temperature / humidity / soil / rain thresholds, dry and wet soil calibration

### Screenshots

**Main Dashboard**

![Main Dashboard](docs/images/dashboard-main.png)

**Last-Minute Table, Controls and Calibration**

![Dashboard Controls](docs/images/dashboard-controls.png)

### 📲 Telegram Bot Output

![Telegram Bot](docs/images/telegram-bot.png)

## 🔄 10. Working Process

1. Sensors collect environmental and soil information.
2. The ESP32 reads digital and analog sensor outputs.
3. Soil raw value is converted to a percentage using calibration values.
4. Rainfall is detected using the configured analog threshold.
5. The latest 60 readings are stored in memory.
6. The embedded web server provides data as JSON.
7. JavaScript fetches the JSON and updates the dashboard.
8. LED and buzzer operate according to alert conditions.
9. Telegram sends a notification when an alert is triggered.

## 🌐 11. Web Server API Endpoints

The ESP32 hosts an HTTP server on port 80.

| Endpoint | Method | Function |
|---|---|---|
| `/` | GET | Loads the dashboard |
| `/data` | GET | Returns readings, configuration and history as JSON |
| `/set` | GET | Updates alert thresholds |
| `/mode` | GET | Changes LED and buzzer modes |
| `/cal` | GET | Performs soil calibration |

Example: `http://ESP32_LOCAL_IP/data`

## ⏱️ 12. Sampling and Data Storage

| Parameter | Configuration |
|---|---|
| Sensor sampling interval | 10 seconds |
| Dashboard refresh interval | 20 seconds |
| Maximum history | 60 readings |
| Total history duration | 10 minutes |
| Soil sensor averaging | 10 analog samples |
| Serial Monitor baud rate | 115200 |
| HTTP server port | 80 |
| Telegram alert cooldown | 5 minutes |

History is kept in RAM (lost on reset); configuration is saved with ESP32 Preferences.

## 🚨 13. Alert Mechanism

**LED**
- AUTO: on during soil or rain alerts
- ON: always on
- OFF: always off

**Buzzer**
- AUTO: beeps during soil or rain alerts
- ON: beeps continuously in repeating intervals
- OFF: silent

**Telegram**
- Sends a startup notification with the dashboard IP
- Sends a notification when a configured alert begins
- Not affected by LED / buzzer OFF mode

> **Note:** In the current firmware, temperature and humidity limits generate dashboard warnings only. LED, buzzer and Telegram alerts are triggered by rainfall or low soil moisture.
>
> Set the **Soil alert below** slider above 0% to enable the low-soil alert.

## 🧪 14. Soil Calibration

Soil sensor readings vary with sensor and soil type.

1. Keep the sensor in dry soil / air → click **Set current soil as dry**.
2. Place it in wet soil / water → click **Set current soil as wet**.

Values are saved in ESP32 Preferences.

## 🛠️ 15. Troubleshooting

| Problem | Possible Solution |
|---|---|
| ESP32 not connecting to Wi-Fi | Verify SSID and password |
| Dashboard not opening | Check ESP32 IP and that you are on the same Wi-Fi |
| DHT11 error | Check DATA, VCC and GND |
| Soil readings incorrect | Perform dry and wet calibration |
| Rain detection incorrect | Adjust rain threshold |
| Telegram not working | Check internet, bot token and chat ID (send `/start` to the bot first) |
| ESP32 not uploading | Check COM port and board selection (hold BOOT while uploading if needed) |

## 📁 16. Repository Structure

```text
Smart-Agriculture-Monitoring/
├── Smart_Agriculture.ino
├── README.md
├── LICENSE
└── docs/
    ├── images/
    │   ├── wiring-diagram.png
    │   ├── dashboard-main.png
    │   ├── dashboard-controls.png
    │   └── telegram-bot.png
    └── video/
        └── demo.mp4
```

## 🗓️ 17. Project Development Timeline

| Phase | Activity | Status |
|---|---|---|
| Phase 1 | Planning and component selection | ✅ Completed |
| Phase 2 | ESP32 and sensor interfacing | ✅ Completed |
| Phase 3 | Data collection and processing | ✅ Completed |
| Phase 4 | Web server and JSON integration | ✅ Completed |
| Phase 5 | Responsive dashboard | ✅ Completed |
| Phase 6 | LED and buzzer alerts | ✅ Completed |
| Phase 7 | Telegram integration | ✅ Completed |
| Phase 8 | Testing and calibration | 🔄 Update after testing |
| Phase 9 | Documentation and GitHub deployment | 🔄 In progress |

## 🔮 18. Future Enhancements

- GPS-based field location tracking
- Soil nutrient and pH sensors
- Cloud-based data storage
- Machine Learning-based crop recommendations
- Crop-specific threshold configuration
- Historical data analysis and reporting
- Automated irrigation control

## 👨‍💻 19. Author

**Teja Sai Gudla**
Electronics and Communication Engineering
GitHub: [TEJA-100](https://github.com/TEJA-100)

## 📄 20. License

This project is released under the MIT License. Add a `LICENSE` file to the repository.

---

**Smart Agriculture Monitoring System – Monitor. Analyze. Improve. 🌱**
