# Print Center Queue Counter (AI-Based People Counting)

## Project Overview
This project provides a real time counter for the Architectural Association Bar, using an Pressure sensor to detect the number of people in the queue. The system consists of:
- **ESP32 ** to count people in the queue.
- **A Node.js backend** to process and store queue data.
- **A p5.js frontend** (widget & UI) to display queue updates to users in real-time.

---

## Project Structure
```
AA Bar Que
   frontend/       # p5.js frontend
   backend/        # Node.js backend
   arduino/        # Arduino sketch for ESP32 with FSR402 pressure sensor
   README.md       # This documentation file
```

---

## Required Components
### **Hardware Components**
  **ESP32 – Microcontroller for handling sensor input and WiFi communication.
  **FSR402 - Detect varying pressure
  **Power Source** – ESP32 requires 5V power supply.
  **WiFi Network** – Required for ESP32 to send data to the backend.  

### **Software Requirements**
  **Arduino IDE** – To flash ESP32 firmware.  
  **Node.js (Backend Server)** – Processes queue data and serves it to the frontend.  
  **p5.js (Frontend UI)** – Displays queue count live.  

---

## Required Libraries

### **p5.js (Frontend UI)**
- [`p5.serialport`](https://github.com/p5-serial/p5.serialport) → Serial communication with Arduino.
- [`socket.io-client`](https://socket.io/docs/v4/client-api/) → WebSockets for real-time queue updates.

### **Node.js (Backend Server)**
- [`express`](https://www.npmjs.com/package/express) → Handles HTTP requests.
- [`socket.io`](https://www.npmjs.com/package/socket.io) → WebSockets for real-time updates.
- [`body-parser`](https://www.npmjs.com/package/body-parser) → Parses incoming queue data.
- [`cors`](https://www.npmjs.com/package/cors) → Allows cross-origin requests from frontend.

### **Arduino (ESP32)**
- [`WiFi`](https://www.arduino.cc/en/Reference/WiFi) → Connects ESP32 to the internet.
- [`ArduinoJson`](https://arduinojson.org/) → Formats queue data as JSON.

  
- FSR402-Specific Functions
Analog Read (analogRead(pin)) → Used to read values from the FSR402 sensor. No external library required.



---

How the System Works (FSR402 Pressure Sensor for Queue Detection)
1. Pressure Detection (FSR402 Sensor)
* The FSR402 sensor is placed on the floor where people queue (e.g., under a mat or taped to the surface).
* When a person steps on the sensor, it changes resistance based on applied pressure.
* The ESP32 reads the analog voltage from the sensor to determine whether a person is present.
2. Data Processing (ESP32 Microcontroller)
* The ESP32 continuously reads the FSR sensor values.
* If the pressure value exceeds a threshold, the system counts a person as present.
* If the pressure drops below the threshold, the system decrements the queue count.
* The ESP32 formats this count into JSON data and prepares it for transmission.
3. Data Transmission (Wi-Fi & HTTP Request)
* The ESP32 connects to Wi-Fi and sends the queue count to a backend server via an HTTP request.
* If Wi-Fi is disconnected, the ESP32 attempts to reconnect automatically.
4. Backend Processing (Node.js Server)
* The Node.js backend receives the queue count from the ESP32.
* It updates the queue count and stores it in a database (MongoDB, optional).
* It broadcasts the updated count to the frontend using WebSockets.
5. Real-Time Display (p5.js Frontend)
* The frontend, built with p5.js, connects to the backend via WebSockets.
* It displays the live queue count on a user interface.
* Optional features like sound alerts, vibration, and notifications can be enabled when the queue changes.

---# de2025_Phalat_Luangsomboon
