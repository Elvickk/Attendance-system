# Quick Start Guide

## Immediate Next Steps

### 1. Configure Wi-Fi
Edit `esp32-firmware/credentials.h`:
```cpp
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
const char* serverUrl = "http://YOUR_PC_IP:3000";
```

### 2. Install Server Dependencies
```bash
cd server
npm install
npm start
```

### 3. Upload ESP32 Firmware
- Open `esp32-firmware/attendance_system.ino` in Arduino IDE
- Install required libraries (MFRC522, LiquidCrystal_I2C)
- Upload to ESP32

### 4. Access Dashboard
Open browser to: http://localhost:3000

### 5. Register First Student
- Click "+ Add Student" on dashboard
- Enter name and scan RFID card
- Test by scanning the card

## File Locations

- **ESP32 Code**: `esp32-firmware/attendance_system.ino`
- **Server**: `server/server.js`
- **Dashboard**: `dashboard/index.html`
- **Database**: Auto-created in `database/attendance.db`

## Key Features Implemented

✅ ESP32 firmware with RFID reading
✅ LCD display integration  
✅ Wi-Fi communication
✅ Node.js/Express backend
✅ SQLite database
✅ Real-time web dashboard
✅ Student management
✅ Attendance tracking with timestamps
✅ Auto-refreshing data

## Hardware Connections

**RC522 RFID Module:**
- SDA → GPIO 21
- SCK → GPIO 18  
- MOSI → GPIO 23
- MISO → GPIO 19
- RST → GPIO 22

**LCD Display (I2C):**
- SDA → GPIO 4
- SCL → GPIO 5

## Support

For detailed setup instructions, see `SETUP_GUIDE.md`