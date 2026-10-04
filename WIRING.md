# Wiring Diagram

## RC522 RFID Module to ESP32

```
RC522 Pin    ESP32 Pin    Color (suggested)
---------    ----------    -----------------
SDA          GPIO 21       Yellow
SCK          GPIO 18       Green
MOSI         GPIO 23       Blue
MISO         GPIO 19       Orange
RST          GPIO 22       Purple
3.3V         3.3V          Red
GND          GND           Black
```

## LCD Display (I2C) to ESP32

```
LCD Pin      ESP32 Pin    Color (suggested)
-------      ----------    -----------------
SDA          GPIO 4        Yellow
SCL          GPIO 5        Green
VCC          5V            Red
GND          GND           Black
```

## Power Considerations

- **ESP32**: Power via USB (5V)
- **RC522**: Use 3.3V from ESP32
- **LCD**: Use 5V from ESP32
- **Common Ground**: Connect all GND pins together

## Connection Order

1. First connect all ground (GND) connections
2. Connect power supplies (3.3V, 5V)
3. Connect data signals (SDA, SCK, MOSI, MISO, RST, SCL)
4. Double-check all connections before powering on

## Testing Connections

### Test RFID Module
- Upload RFID test sketch
- Open Serial Monitor (115200 baud)
- Bring card near reader
- Should see UID in serial monitor

### Test LCD Display
- Upload I2C scanner sketch
- Check serial monitor for I2C address
- Upload LCD test sketch
- Should see text on display

## Common Issues

**RFID not reading:**
- Check 3.3V power supply
- Verify all SPI connections
- Ensure proper grounding

**LCD not displaying:**
- Check I2C address (0x27 or 0x3F)
- Verify SDA/SCL connections
- Check 5V power supply

**ESP32 not booting:**
- Check USB cable (use data cable, not charge-only)
- Verify correct COM port selected
- Try pressing BOOT button during upload