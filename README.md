### README.md

```markdown
# IoT Monitoring System

This project is an IoT-based monitoring system that collects environmental data (water temperature, air temperature, humidity, and pH level) using sensors connected to an Arduino board. The collected data is sent to a Raspberry Pi for processing, storage on ThingSpeak, and alerts via Telegram.

---

## Features
1. **Data Collection**:
   - **Sensors**:
     - DS18B20: Measures water temperature.
     - DHT21: Measures air temperature and humidity.
     - pH Sensor: Measures water pH levels.
   - The Arduino board reads data from the sensors and sends it to the Raspberry Pi via serial communication.

2. **Data Processing**:
   - The Raspberry Pi processes the received data and:
     - Sends it to [ThingSpeak](https://thingspeak.com/) for visualization.
     - Sends real-time alerts to a specified Telegram group if:
       - Water temperature is outside the range of 20°C to 25°C.
       - pH level is outside the range of 7 to 7.5.

3. **Telegram Integration**:
   - Users can request the latest sensor data by sending the message `gui` in the Telegram group.

---

## System Architecture
1. **Hardware**:
   - Arduino with DS18B20, DHT21, and pH sensor.
   - Raspberry Pi as the central controller.

2. **Software**:
   - **Python** on Raspberry Pi:
     - Reads sensor data from Arduino via serial communication.
     - Uploads data to ThingSpeak.
     - Sends alerts via Telegram.
   - **Arduino Code**:
     - Collects sensor data and sends it to Raspberry Pi.

---

## Installation and Setup
### **1. Hardware Setup**
- Connect the DS18B20, DHT21, and pH sensors to the Arduino according to their pin specifications.
- Connect the Arduino to the Raspberry Pi via USB.

### **2. Arduino Configuration**
- Upload the provided `Arduino` code (`.ino`) to the Arduino using the Arduino IDE.

### **3. Raspberry Pi Configuration**
- Install the required Python libraries:
  ```bash
  pip install pyserial requests python-telegram-bot
  ```
- Update the Raspberry Pi script with your:
  - `THINGSPEAK_API_KEY`
  - `TELEGRAM_BOT_TOKEN`
  - `TELEGRAM_CHAT_ID`
- Run the Python script on the Raspberry Pi:
  ```bash
  python3 script.py
  ```

### **4. Telegram Setup**
- Create a Telegram bot using [BotFather](https://t.me/BotFather) and get the bot token.
- Add the bot to a group and note the group chat ID.

---

## Usage
- **Data Upload**:
  - Data is automatically sent to ThingSpeak every 15 seconds.
- **Alerts**:
  - Alerts are sent to Telegram when:
    - Water temperature is out of range (20°C - 25°C).
    - pH level is out of range (7 - 7.5).
- **Manual Data Request**:
  - Send the message `gui` in the Telegram group to receive the latest data from the sensors.

---

## Code Overview
### **Python Script (Raspberry Pi)**
- Handles serial communication with Arduino.
- Sends data to ThingSpeak and Telegram.
- Processes alerts based on sensor thresholds.

### **Arduino Code**
- Reads data from sensors and sends it to Raspberry Pi in the format:
  ```
  <water_temp>,<air_temp>,<humidity>,<pH_value>
  ```

---

## Dependencies
- Python 3.x
- Libraries:
  - `serial`
  - `requests`
  - `python-telegram-bot`

---

## Example Output
### **ThingSpeak Dashboard**
- Visualizes real-time and historical data for:
  - Water Temperature
  - Air Temperature
  - Humidity
  - pH Value

### **Telegram Alerts**
- Example:
  ```
  Alert: Water temperature is high: 26°C!
  Alert: pH level is high: 8.0!
  ```

- On sending `gui`:
  ```
  Water Temperature: 22°C
  Air Temperature: 25°C
  Humidity: 55%
  pH Value: 7.2
  ```

---

## Future Improvements
- Add more sensors for extended monitoring capabilities.
- Integrate with other IoT platforms like AWS IoT or Google Cloud IoT.
- Improve the user interface for data visualization.
