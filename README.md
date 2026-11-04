# 📡 DeautherX — ESP8266 WiFi Deauthenticator

> ⚠️ **DISCLAIMER**: This project is intended **solely for educational purposes** and authorized penetration testing on networks you own or have explicit written permission to test. Unauthorized use of deauthentication attacks is **illegal** in most countries. The author assumes **no liability** for misuse.

---

## 📋 Overview

**DeautherX** is an ESP8266-based WiFi deauthentication tool that leverages the IEEE 802.11 management frame injection capabilities of the ESP8266 chip. It allows you to scan nearby WiFi networks, monitor connected stations, and perform deauthentication packet injection for testing network resilience.

Built on top of the [ESP8266 Deauther](https://github.com/SpacehuhnTech/esp8266_deauther) framework with improvements and fixes.

---

## ✨ Features

- 📶 **WiFi Scanning** — Discover nearby access points and connected stations
- 🚫 **Deauth Attack** — Send 802.11 deauthentication frames
- 📋 **CLI Interface** — Serial command-line interface for control
- 🖥️ **Display Support** — OLED display UI support
- 💾 **Persistent Settings** — Save/load config via EEPROM & LittleFS
- 🌐 **Web Interface** — Built-in access point with web UI
- 🔁 **Auto-save** — Periodic automatic saving of configuration
- 🔘 **Reset Button** — Hardware button to reset settings
- 💡 **LED Indicator** — Visual status feedback via LED

---

## 🛠️ Hardware Requirements

| Component | Specification |
|-----------|--------------|
| Microcontroller | ESP8266 (NodeMCU v1.0 / Wemos D1 Mini) |
| Flash Memory | ≥ 1MB (4MB recommended) |
| Display (optional) | SSD1306 OLED (128x64, I2C) |
| Button (optional) | Tactile push button for reset |
| LED (optional) | RGB or single-color LED |

---

## 📦 Software Requirements

### Arduino IDE Setup
1. Install [Arduino IDE](https://www.arduino.cc/en/software) (1.8.x or 2.x)
2. Add ESP8266 board support:
   - Go to **File → Preferences**
   - Add this URL to "Additional Boards Manager URLs":
     ```
     https://arduino.esp8266.com/stable/package_esp8266com_index.json
     ```
   - Go to **Tools → Board → Boards Manager**, search for `esp8266` and install

### Required Libraries

Install via **Tools → Manage Libraries**:

| Library | Version | Notes |
|---------|---------|-------|
| **ArduinoJson** | `5.x` ⚠️ | Must be v5, NOT v6 or v7 |
| **StringSplitter** | Latest | Search "StringSplitter" |
| **SimpleButton** | Latest | For reset button support |

> ⚠️ **Important**: ArduinoJson must be version **5.x**. The code will not compile with v6 or v7.

---

## 🚀 Installation & Flashing

1. **Clone this repository**
   ```bash
   git clone https://github.com/adithyanp2005gt-dotcom/DeautherX.git
   cd DeautherX
   ```

2. **Open in Arduino IDE**
   - Open `DeautherX.ino`

3. **Select Board Settings**
   - **Board**: `NodeMCU 1.0 (ESP-12E Module)` or your ESP8266 variant
   - **Flash Size**: `4MB (FS: 2MB, OTA: ~1019KB)`
   - **CPU Frequency**: `80 MHz`
   - **Upload Speed**: `115200`

4. **Install Libraries** (see above)

5. **Flash the board**
   - Connect your ESP8266 via USB
   - Click **Upload** (Ctrl+U)

---

## ⚙️ Configuration

Edit `A_config.h` before compiling to customize:

```cpp
#define RESET_BUTTON  // GPIO pin for the reset button
#define HIGHLIGHT_LED // Enable LED highlight on boot
#define FORMAT_SPIFFS // Uncomment to format filesystem on next boot
#define FORMAT_EEPROM // Uncomment to format EEPROM on next boot
#define RESET_SETTINGS // Uncomment to reset all settings on next boot
```

---

## 📡 Usage

### Web Interface
1. After flashing, the ESP8266 creates a WiFi access point
2. Connect to it (default SSID/password in `settings.h`)
3. Open `192.168.4.1` in your browser

### Serial CLI
1. Open Serial Monitor at **115200 baud**
2. Type `help` to see available commands

### Reset Button
- **Double-click**: Shut down display
- **Hold 3 seconds**: Reset all settings to defaults

---

## 📁 Project Structure

```
DeautherX/
├── DeautherX.ino       # Main sketch entry point
├── A_config.h          # Hardware/compile-time configuration
├── Attack.h/.cpp       # Deauth attack logic
├── CLI.h/.cpp          # Serial command-line interface
├── DisplayUI.h/.cpp    # OLED display UI
├── EEPROMHelper.h      # EEPROM read/write helpers
├── functions.h         # Utility functions
├── language.h          # String constants / localization
├── led.h               # LED control
├── Names.h/.cpp        # Saved device name management
├── oui.h               # OUI vendor lookup table
├── Scan.h/.cpp         # WiFi scanning logic
├── settings.h/.cpp     # Settings management
├── SSIDs.h/.cpp        # SSID list management
├── wifi.h              # WiFi AP/station management
└── src/
    └── ArduinoJson-v5.13.5/  # Bundled ArduinoJson v5
```

---

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| `StringSplitter.h: No such file` | Install StringSplitter from Library Manager |
| `ArduinoJSON version` compile error | Downgrade ArduinoJson to version 5.x |
| Upload fails | Hold FLASH button while clicking Upload |
| LittleFS mount error | Board will auto-format on boot-loop detection |
| Web UI not loading | Ensure flash size has FS partition allocated |

---

## ⚖️ Legal Notice

This tool is provided for **educational and authorized security research only**. By using this software, you agree that:

- You will only use this tool on networks you **own** or have **explicit written authorization** to test
- You understand that unauthorized deauthentication attacks are **illegal** under laws such as the CFAA (USA), Computer Misuse Act (UK), and similar legislation worldwide
- The developer is **not responsible** for any illegal or unethical use

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgements

- [SpacehuhnTech](https://github.com/SpacehuhnTech) for the original ESP8266 Deauther
- [ESP8266 Community](https://github.com/esp8266/Arduino) for the Arduino core
- [ArduinoJson](https://arduinojson.org/) by Benoit Blanchon
