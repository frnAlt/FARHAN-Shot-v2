# FARHAN-Shot v2 - WiFi WPS Security Testing Tool

## Overview

FARHAN-Shot v2 is a WiFi WPS (WiFi Protected Setup) security testing framework designed for penetration testing and security research. The tool automates WPS PIN attacks using multiple attack vectors including Pixie Dust, NULL PIN fallback, and online brute force methods. It targets vulnerable routers with a database of 576+ known vulnerable devices and supports modern WiFi standards (WiFi 4/5/6) with WPA3 detection capabilities.

**Primary Purpose**: Automated WPS vulnerability assessment and PIN-based network security testing for authorized penetration testing scenarios.

**Target Platforms**: Android (rooted) and Linux systems, with special optimizations for Termux environment.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Core Design Pattern
- **Modular Script Architecture**: Multiple Python scripts serving different purposes (main attack engine, setup, updates, vulnerability database)
- **No Framework Dependencies**: Pure Python implementation with minimal external dependencies beyond system utilities
- **Command-Line Interface**: Direct execution model without web servers or GUI components

### Attack Engine Architecture

**Main Attack Flow** (`main.py`, `File/advance-Shot.py`, `File/FARHAN-Shotx.py`):
1. Network discovery using `wpa_supplicant` (no monitor mode required)
2. Device fingerprinting against vulnerability database (`vulnwsc.txt`)
3. Multi-vector attack execution:
   - Pixie Dust attack (primary)
   - NULL PIN fallback (00000000)
   - Database PIN lookup
   - Online brute force
4. Extended timeout system for long-distance attacks (RSSI < -75 dBm)
5. Credential extraction and storage

**Key Architectural Decisions**:
- **wpa_supplicant over Monitor Mode**: Chosen for maximum compatibility across Android and Linux without requiring special wireless card capabilities. Trade-off: Some attack vectors unavailable but broader device support achieved.
- **Multiple Attack Scripts**: Various implementations (3FRN.py, advance-Shot.py, FARHAN-Shotx.py, oneshot.py) provide different attack strategies and backward compatibility options.

### Data Storage Architecture

**Vulnerability Database** (`vulnwsc.txt`):
- Flat-file text format containing 576+ vulnerable device models
- Simple line-by-line parsing for quick lookups
- Device entries include model names and version numbers
- Manual curation with duplicate removal logic in `vulnwsc.py`

**Credential Storage** (`store/FARHAN-Shot_crack_data.txt`):
- Append-only text file for captured credentials
- Format: SSID, PIN, PSK with timestamp
- Directory auto-creation on first write
- No encryption (security note: sensitive data stored in plaintext)

**Design Decision**: Flat-file storage chosen over database for simplicity and portability. No external database dependencies required, but lacks query optimization for large datasets.

### Color/UI System

**Terminal Color Management** (`colors.py`):
- ANSI escape code constants for cross-platform terminal coloring
- Dual naming convention (lowercase and uppercase) for backward compatibility
- No external colorama dependency in core (though imported in `vulnwsc.py`)

### Installation & Update System

**Package Management** (`setup.py`):
- Termux-specific installation script
- Python package structure setup
- Binary/executable creation in PREFIX/bin
- Version detection and path configuration

**Update Mechanism** (`update.py`):
- Git-based update system
- Requires .git directory presence
- Direct git pull execution with error handling
- No version checking or rollback capability

**Design Decision**: Git-based updates chosen for simplicity. Trade-off: Requires git installation and network access, but ensures latest code availability.

### WiFi Standard Detection

**Modern WiFi Support**:
- WiFi 6 (802.11ax) detection
- WPA3/SAE protocol identification
- Mixed WPA2/WPA3 network handling
- RSSI-based timeout adjustment for weak signals

**Implementation**: Parsing of `wpa_supplicant` output and network scan results to identify protocol versions and security modes.

### Code Organization

**Script Variants**:
- `main.py`: Entry point and core logic
- `File/advance-Shot.py`: Advanced attack logic with custom PIN support
- `File/FARHAN-Shotx.py`: Extended version with additional options
- `File/3FRN.py`: Alternative implementation
- `File/oneshot.py`: Standalone attack script
- `File/FARHAN-Shot.py`: Compiled/obfuscated version using marshal

**Design Pattern**: Multiple script variants provide flexibility but create maintenance overhead. Each script is largely self-contained with duplicated core logic.

## External Dependencies

### System-Level Dependencies
- **wpa_supplicant**: Core WiFi management and WPS attack execution
- **Linux Kernel WiFi Drivers**: Required for wireless interface control
- **Root/Superuser Access**: Necessary for low-level network operations

### Python Environment
- **Python 3.6+**: Minimum version requirement
- **Standard Library Only**: Core functionality uses only built-in modules (subprocess, os, sys, re, time, datetime, collections, statistics, csv, pathlib, socket, tempfile, shutil, codecs)
- **Optional**: colorama (used in vulnwsc.py for enhanced terminal colors)

### Platform-Specific Dependencies
- **Termux (Android)**: PREFIX environment variable, pkg package manager
- **Git**: Required for update functionality
- **Root Access**: Mandatory for wireless interface manipulation on Android

### Network Tools
- **wpa_cli**: WPA supplicant command-line interface
- **iw/iwconfig**: Wireless interface configuration utilities (platform-dependent)

### Data Files
- `vulnwsc.txt`: Vulnerability database (576+ device entries)
- `config.txt`: Configuration file (removed for security, currently empty)
- No external API calls or cloud services

**Security Note**: Tool operates entirely offline once installed. No telemetry, analytics, or external service dependencies.