# Setup Guide - Smart Attendance System

## Prerequisites

### Hardware
- ESP32 development board
- RC522 RFID module
- LCD 16x2 with I2C adapter
- Breadboard and jumper wires
- USB cable for ESP32 programming
- RFID cards (Mifare 13.56 MHz)

### Software
- Arduino IDE (latest version)
- Node.js (v14 or higher)
- Web browser (Chrome, Firefox, Edge)

## Step-by-Step Setup

### 1. Hardware Connections

#### RC522 RFID Module to ESP32:
```
RC522    ESP32
------   -----
SDA  ->  GPIO 21
SCK  ->  GPIO 18
MOSI ->  GPIO 23
MISO ->  GPIO 19
RST  ->  GPIO 22
3.3V ->  3.3V
GND  ->  GND
```

#### LCD Display (I2C) to ESP32:
```
LCD    ESP32
---    -----
SDA ->  GPIO 4
SCL ->  GPIO 5
VCC ->  5V
GND ->  GND
```

### 2. Arduino IDE Setup

1. Install Arduino IDE from [arduino.cc](https://www.arduino.cc/en/software)
2. Add ESP32 board support:
   - Open Arduino IDE
   - Go to File → Preferences
   - Add this URL to "Additional Board Manager URLs":
     ```
     https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
     ```
3. Install ESP32 boards:
   - Go to Tools → Board → Boards Manager
   - Search for "ESP32"
   - Install "ESP32 by Espressif Systems"

### 3. Install Arduino Libraries

Install these libraries via Sketch → Include Library → Manage Libraries:

1. **MFRC522** by Miguel Balboa
2. **LiquidCrystal_I2C** by Frank de Brabander

### 4. Configure ESP32 Firmware

1. Open `esp32-firmware/attendance_system.ino` in Arduino IDE
2. Edit `esp32-firmware/credentials.h`:
   ```cpp
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";
   const char* serverUrl = "http://YOUR_PC_IP:3000";
   ```
3. Find your PC's IP address:
   - Windows: Open Command Prompt, run `ipconfig`
   - Look for "IPv4 Address" (e.g., 192.168.1.100)
4. Update `serverUrl` with your PC's IP address

### 5. Upload ESP32 Firmware

1. Select ESP32 board: Tools → Board → ESP32 Dev Module
2. Select correct COM port: Tools → Port → COMx
3. Click Upload button (→)
4. Wait for upload to complete

### 6. Server Setup

1. Install Node.js from [nodejs.org](https://nodejs.org/)
2. Open terminal/command prompt
3. Navigate to server directory:
   ```bash
   cd "C:\Users\user\Desktop\Attendance system\server"
   ```
4. Install dependencies:
   ```bash
   npm install
   ```
5. Start the server:
   ```bash
   npm start
   ```
6. Server will start on http://localhost:3000

### 7. Access Dashboard

1. Open web browser
2. Navigate to: http://localhost:3000
3. You should see the attendance dashboard

### 8. Register Students

1. On the dashboard, click "+ Add Student"
2. Enter student name and ID (optional)
3. Scan RFID card or enter UID manually
4. Click "Add Student"
5. Repeat for all students

### 9. Test Attendance System

1. Ensure ESP32 is powered and connected to WiFi
2. LCD should show "Ready to Scan"
3. Scan a registered RFID card
4. LCD should show student name and "Marked Present"
5. Dashboard should update automatically with new attendance record

## Troubleshooting

### ESP32 won't connect to WiFi
- Check WiFi credentials in credentials.h
- Ensure ESP32 is within WiFi range
- Try 2.4GHz network (ESP32 doesn't support 5GHz)

### RFID module not reading cards
- Check wiring connections
- Ensure 3.3V power supply is adequate
- Try different RFID cards

### LCD not displaying
- Check I2C address (default is 0x27, some use 0x3F)
- Verify wiring connections
- Run I2C scanner to find correct address

### Server not accessible from ESP32
- Ensure PC and ESP32 are on same network
- Check Windows Firewall settings
- Try using PC's IP address instead of localhost

### Dashboard not updating
- Check if server is running
- Open browser console (F12) for errors
- Ensure API endpoints are responding

## Advanced Configuration

### Change I2C LCD Address
If your LCD uses a different I2C address:
1. Install I2C scanner sketch
2. Upload to ESP32
3. Check serial monitor for address
4. Update `LCD_ADDRESS` in attendance_system.ino

### Change Server Port
To use a different port:
1. Edit `server/server.js`
2. Change `const PORT = 3000;` to desired port
3. Update `serverUrl` in ESP32 credentials.h

### Custom Timeouts
Adjust these in attendance_system.ino:
- `CARD_READ_DELAY`: Time between card reads (default: 2000ms)

## Security Notes

- Change default passwords and credentials
- Use HTTPS in production
- Implement authentication for dashboard
- Keep firmware and server updated
- Secure RFID cards and prevent cloning