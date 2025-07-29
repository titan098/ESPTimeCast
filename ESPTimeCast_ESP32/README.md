# ESPTimeCast ESP32-C3 PlatformIO Project

This is a PlatformIO conversion of the ESPTimeCast Arduino project, specifically configured for ESP32-C3 microcontrollers.

## Hardware Requirements

- **ESP32-C3 Supermini Development Board**
- **MAX7219/MAX7221 LED Matrix Display** (4 modules)
- **Connections:**
  - CLK: GPIO 7
  - CS: GPIO 6  
  - DATA: GPIO 5

## Features

- **WiFi Clock Display** with NTP synchronization
- **Weather Information** via OpenWeatherMap API
- **Web Configuration Interface** (captive portal in AP mode)
- **Countdown Timer** functionality
- **Multi-language Support** for day names and weather descriptions
- **Brightness Control** and automatic dimming
- **Custom Font** for LED matrix display

## Getting Started

### Prerequisites

- [PlatformIO](https://platformio.org/) installed (via VS Code extension or CLI)
- ESP32-C3 development board
- USB cable for programming

### Building and Uploading

1. **Clone/Download** this project
2. **Open** the project folder in VS Code with PlatformIO extension
3. **Build** the project:
   ```bash
   pio run
   ```
4. **Upload** to ESP32-C3:
   ```bash
   pio run --target upload
   ```
5. **Upload filesystem** (web interface files):
   ```bash
   pio run --target uploadfs
   ```

### First Setup

1. **Power on** the ESP32-C3 with LED matrix connected
2. **Connect** to WiFi network "ESPTimeCast" (password: 12345678)
3. **Open browser** and navigate to `192.168.4.1`
4. **Configure** your WiFi credentials and settings
5. **Save** configuration - device will reboot and connect to your WiFi

## Project Structure

```
├── platformio.ini          # PlatformIO configuration
├── src/
│   ├── main.cpp            # Main application code
│   ├── mfactoryfont.h      # Custom LED matrix font
│   ├── tz_lookup.h         # Timezone mappings
│   └── days_lookup.h       # Multi-language day names
├── data/
│   ├── index.html          # Web configuration interface
│   └── config.json         # Configuration storage
└── README.md               # This file
```

## Configuration

### PlatformIO Configuration (platformio.ini)

- **Target Board:** `supermini_c3` (custom board definition)
- **Framework:** Arduino
- **Build Flags:** Optimized for ESP32-C3 Supermini with USB CDC support
- **Libraries:** All required dependencies automatically installed

### Key Libraries Used

- **MD_Parola** (3.7.x) - LED matrix text display
- **MD_MAX72XX** (3.5.x) - MAX72xx LED matrix driver  
- **ArduinoJson** (7.x) - JSON configuration parsing
- **ESPAsyncWebServer** - Async web server for configuration
- **AsyncTCP** - TCP library for ESP32

### Hardware Configuration

The pin assignments are defined in `src/main.cpp`:
```cpp
#define CLK_PIN 7
#define CS_PIN 6  
#define DATA_PIN 5
```

## Web Interface

Once connected to WiFi, access the web interface at the device's IP address to configure:

- **WiFi Settings**
- **OpenWeatherMap API** (for weather display)
- **Time Zone** and NTP servers
- **Display Options** (brightness, 12/24 hour, etc.)
- **Countdown Timer**
- **Language Settings**

## Development

### Building

```bash
# Build project
pio run

# Build and upload
pio run --target upload

# Upload filesystem
pio run --target uploadfs

# Monitor serial output
pio device monitor
```

### Customization

- **Pin Configuration:** Modify pin definitions in `src/main.cpp`
- **Display Settings:** Adjust scroll speeds and timing constants
- **Font:** Replace `mfactoryfont.h` with custom font data
- **Languages:** Add entries to `days_lookup.h` for additional languages

## Troubleshooting

### Build Issues

- Ensure PlatformIO is up to date
- Clean build: `pio run --target clean`
- Check ESP32 platform version in `platformio.ini`

### Upload Issues

- Verify ESP32-C3 is in download mode (hold BOOT button while connecting USB)
- Check USB cable supports data transfer
- Try different upload speeds in `platformio.ini`

### Runtime Issues

- Monitor serial output: `pio device monitor`
- Check WiFi credentials in web interface
- Verify LED matrix wiring and power supply
- Ensure OpenWeatherMap API key is valid (32 characters)

## License

This project maintains the same license as the original ESPTimeCast project.

## Credits

- Original ESPTimeCast project by MFactory Osaka
- PlatformIO conversion and ESP32-C3 optimization
- Libraries by their respective authors (see platformio.ini)
