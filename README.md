# FARHAN-Shot v2 - Advanced WiFi WPS Security Testing Tool

<div align="center">

**Modern WiFi Security Testing Framework with 2025 Attack Capabilities**

[![Python Version](https://img.shields.io/badge/Python-3.6%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-GPL--3.0-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20Linux-orange.svg)](https://github.com)
[![WiFi Standard](https://img.shields.io/badge/WiFi-4%20%7C%205%20%7C%206-red.svg)](https://www.wi-fi.org/)

</div>

## 🔥 What's New in v2 (2025 Edition)

### 🚀 Modern Attack Capabilities
- **WiFi 6 (802.11ax) Support**: Full detection and testing of WiFi 6 routers
- **WPA3/SAE Detection**: Identify WPA3 networks and mixed WPA2/WPA3 deployments
- **Universal WiFi Scanning**: Android-style network discovery with automatic fallback
- **NULL PIN Auto-Fallback**: Never fail with "no PIN found" errors again (auto-tries 00000000)
- **Extended Timeout System**: Optimized for long-distance attacks (RSSI < -75 dBm)
- **576+ Device Database**: Massive expansion with modern 2023-2025 routers

### 📡 Enhanced Device Support (576 Total Devices)
- **TP-Link**: Archer AX10/20/50/55/73/75/90/96, Deco X20/X50/X60/X90, RE700X/815X
- **Xiaomi/Redmi**: AX1800/3000/3200/3600/5/5400/6000/6S/9000 (all modern AX series)
- **Netgear**: RAX10/15/20/30/35/38/40/43/45/48/50/70/75/78/80/120/200, Nighthawk AX series
- **ASUS**: RT-AX53U/55/56U/57/58U/59U/68U/82U/86U/86S/88U/89X/92U, TUF-AX3000/4200/5400
- **D-Link**: DIR-X1560/1860/3260/4860/5460/6060, EAGLE PRO AI AX series
- **Huawei/Honor**: AX2/AX3/AX3 Pro, WiFi AX2/AX3, Honor Router 3/4/X3/X3 Pro
- **ZTE**: AX1800/3000/3000 Pro/5400, MC7010/MC888
- **Tenda**: AX3/AX9/AX12/AX1803/AX3000, AC6/8/9/10/15/18/19/21/23
- **Other**: Linksys, Mercusys, Totolink, Cudy, Ubiquiti UniFi 6, Keenetic, Google Nest WiFi Pro, Amazon eero 6 series

---

## 📖 Overview

**FARHAN-Shot v2** is a powerful WPS (WiFi Protected Setup) security testing tool designed for penetration testers, security researchers, and network administrators. It automates WPS PIN attacks using multiple attack vectors without requiring monitor mode.

### Core Features

✅ **No Monitor Mode Required** - Uses wpa_supplicant for compatibility  
✅ **Multiple Attack Vectors** - Pixie Dust, NULL PIN, Online Bruteforce  
✅ **Intelligent PIN Database** - 576+ vulnerable routers with known PINs  
✅ **Automatic Fallback** - NULL PIN (00000000) when no specific PIN found  
✅ **WiFi Standard Detection** - Identifies WiFi 4/5/6 and security protocols  
✅ **WPA3 Detection** - Shows WPA3/SAE and mixed WPA2/WPA3 networks  
✅ **Long-Distance Optimized** - Extended timeouts for weak signals (RSSI < -75 dBm)  
✅ **Android & Linux Support** - Works on rooted Android with universal WiFi fetch  

---

## 🔧 Requirements

### System Requirements
- **Operating System**: Linux (Ubuntu, Kali, Parrot) or Rooted Android
- **Python**: 3.6 or higher
- **Root Access**: Required for WiFi operations
- **WiFi Adapter**: Any adapter supporting wpa_supplicant

### Dependencies
```bash
# Core tools (auto-installed via installer.sh)
- wpa_supplicant
- iw / iwconfig (Android: cmd wifi / dumpsys wifi)
- python3
- python3-pip
```

---

## 📥 Installation

### Method 1: Automated Installation (Recommended)

```bash
# Clone the repository
git clone https://github.com/Gtajisan/FARHAN-Shot-v2.git
cd FARHAN-Shot-v2

# Run the installer (requires root)
sudo bash installer.sh
```

### Method 2: Manual Installation

```bash
# Clone repository
git clone https://github.com/Gtajisan/FARHAN-Shot-v2.git
chmod +x FARHAN-Shot-v2/main.py
```
# Install system dependencies
```bash
sudo apt update
sudo apt install -y wpasupplicant iw net-tools
```

### Method 3: Android Installation (Termux)

```bash
# Install Termux and Termux:API from F-Droid
pkg update && pkg upgrade -y
pkg install root-repo -y
pkg install git tsu python wpa-supplicant iw -y

# Clone and setup
git clone https://github.com/Gtajisan/FARHAN-Shot-v2.git
chmod +x FARHAN-Shot-v2/main.py

```

---

## 🎯 Usage

### Quick Start

```bash
# Launch FARHAN-Shot (requires root)
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -K

# Or use the wrapper script
sudo ./FARHAN-Shot.sh

# Scan for WPS-enabled networks
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 --scan
```

### Command Examples

```bash
# Scan WiFi networks and show WPS status
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 --scan

# Attack specific BSSID with Pixie Dust
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> -K

# Attack with NULL PIN fallback (auto-enabled)
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> --pixie-mode

# Use custom PIN
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> --pin 12345670

# Bruteforce with PIN prefix
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> -B -p 1234

# Verbose mode for debugging
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> -K --verbose
```

---

## ⚙️ Attack Modes

### 1. Pixie Dust Attack (Offline) ⚡
**Fast and effective against vulnerable routers**
- Exploits weak random number generation in WPS
- Works offline without network authentication
- Success rate: ~30-40% on vulnerable devices
- Time: 5-30 seconds

```bash
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> -K
```

### 2. NULL PIN Attack (Auto-Fallback) 🔓
**Bypass for routers with known NULL PIN vulnerability**
- Automatically tries PIN 00000000 when no specific PIN found
- Works on 2019-2025 routers with default configurations
- Success rate: ~10-15% on modern routers
- Time: Instant

*Automatically enabled when no PIN database match found*

### 3. Online Bruteforce 🔨
**Traditional PIN bruteforce attack**
- Tests all PINs from database sequentially
- Slower but comprehensive
- Success rate: ~50-60% if device in database
- Time: 2-6 hours (depends on rate limiting)

```bash
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -b <BSSID> -B
```

---

## 📊 WiFi 6 & WPA3 Detection

FARHAN-Shot v2 automatically detects modern WiFi standards:

```
BSSID             ESSID           Security    WiFi Standard       WPS
──────────────────────────────────────────────────────────────────────
AA:BB:CC:DD:EE:FF MyRouter_5G     WPA2/WPA3   WiFi 6 (802.11ax)  [✓]
11:22:33:44:55:66 OldRouter       WPA2        WiFi 5 (802.11ac)  [✓]
```

**WPA3 Notice**: WPA3-only networks typically disable WPS. However, many routers run in WPA2/WPA3 mixed mode where WPS may still be active on the WPA2 band.

---

## 🗄️ Device Database (vulnwsc.txt)

The tool includes an extensive database of **576 vulnerable routers** with known default PINs:

### Database Format
```
Manufacturer Model Version
Example: TP-Link Archer AX55 v1.0
```

### Update Database
```bash
# Pull latest updates
sudo python3 update.py

# Or manually edit
nano vulnwsc.txt
```

---

## 🔍 Advanced Features

### 1. Universal WiFi Fetch (Android) 📱
Automatic fallback when `iw` fails on Android:
```bash
# Uses Android WiFi APIs
cmd wifi list-scan-results
dumpsys wifi | grep -A 20 "Latest scan results"
```

### 2. Extended Timeout for Long Distance 📡
```bash
# Automatically extends timeout for weak signals
# Normal: Standard timeout
# Weak (RSSI < -75 dBm): Extended timeout for long-distance attacks
```

### 3. Smart PIN Generation 🧠
Algorithm-based PIN generation for:
- MAC-based algorithms (pin24, pin28, pin32)
- Vendor-specific (D-Link, ASUS, Realtek, Broadcom)
- Chipset algorithms (Ralink, MediaTek, Qualcomm)

---

## 🛡️ Legal Disclaimer

⚠️ **FOR EDUCATIONAL AND AUTHORIZED TESTING ONLY** ⚠️

This tool is designed for:
- **Authorized penetration testing** with written permission
- **Personal network security auditing** on networks you own
- **Educational research** in controlled environments
- **Security research** with proper authorization

**ILLEGAL USES:**
- ❌ Attacking networks without permission
- ❌ Unauthorized access to WiFi networks
- ❌ Intercepting others' communications

**You are responsible for your actions. The developers assume NO liability for misuse.**

---

## 🐛 Troubleshooting

### Common Issues

**1. "Command failed: No such device"**
```bash
# Check WiFi interface name
iw dev

# Specify interface manually
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -K
```

**2. "Permission denied"**
```bash
# Ensure running with root
sudo python3 FARHAN-Shot-v2/main.py -i wlan0 -K
```

**3. "No PIN found for device"**
```bash
# NULL PIN fallback is automatic
# Tool will try 00000000 when no specific PIN found
```

**4. "WPS locked / Timeout"**
```bash
# Router rate limiting detected
# Wait 5-10 minutes and try again
# Extended timeout activates automatically for weak signals
```

**5. "WiFi 6 not detected"**
```bash
# Ensure adapter supports 802.11ax scanning
# Update iw to latest version
sudo apt update && sudo apt install iw
```

**6. Android: "iw command not found"**
```bash
# Universal WiFi scan activates automatically
# Uses cmd wifi / dumpsys wifi fallback
```

---

## 📝 Project Structure

```
FARHAN-Shot-v2/
├── main.py                 # Main application logic
├── colors.py               # Terminal color output
├── setup.py                # Package setup configuration
├── installer.sh            # Automated installer script
├── FARHAN-Shot.sh          # Launch wrapper script
├── update.py               # Auto-update functionality
├── vulnwsc.txt             # Vulnerable device database (576 entries)
├── requirements.txt        # Python dependencies
├── README.md               # This file
└── LICENSE                 # GPL-3.0 License
```

---

## 🔄 Updates & Maintenance

### Check for Updates
```bash
sudo python3 update.py
```

### Manual Update
```bash
cd FARHAN-Shot-v2
git pull origin main
pip3 install -r requirements.txt --upgrade
```

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Add new devices to vulnwsc.txt**
   - Format: `Manufacturer Model Version`
   - Include chipset info if known

2. **Report bugs**
   - Open an issue with device info and logs

3. **Improve attack algorithms**
   - Submit pull requests with new PIN generation algorithms

---

## 📜 License

This project is licensed under the **GNU General Public License v3.0** - see [LICENSE](LICENSE) file for details.

---

## 👥 Credits

- **Original FARHAN-Shot**: WPS PIN attack framework
- **Porter-union-rom-updates**: Stable base implementation
- **WiFi Security Community**: Attack methodologies and research
- **rofl0r**: Initial implementation
- **Monohrom**: Testing and bug catching
- **Wiire**: Developing Pixiewps
- **DRYGDRYG**: Real developer contributions
- **Mohammad Al Amin**: Source and tool development
- **FARHAN-MUH-TASIM**: Creator and maintainer 📍

---

## 📞 Contact & Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/FARHAN-Shot-v2/issues)
- **Telegram**: [@FARHAN_MUH_TASIM](https://t.me/FARHAN_MUH_TASIM)
- **YouTube**: [Watch Tutorial](https://youtu.be/5janYQg1-Yw)

---

<div align="center">

**Made with ❤️ for the Security Community**

*Stay Ethical. Stay Legal. Stay Secure.*

⭐ **Star this repo if you find it useful!** ⭐

</div>
