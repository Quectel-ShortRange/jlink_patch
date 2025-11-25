# J-Link Device Support Patch

This repository contains J-Link device support patches for Quectel modules with flash memory not natively supported by SEGGER. These patches enable J-Link debuggers to recognize and program these devices by providing device definitions, flash loaders, and initialization scripts.

## Overview

The J-Link Device Support Kit (DSK) allows adding support for new devices to the J-Link software. This repository includes device support files for:

- **FCM363X**
- **FCMA62N**
- **FGMH63X**

## Repository Structure

```
JLinkDevices/
├── JLinkDevices.xml           # Main device database file
└── Devices/
    └── QUECTEL/
        └── <DEVICE_NAME>/
            ├── *.FLM          # Flash loaders
            └── *.JLinkScript  # Device initialization script
```

## Installation

### Method 1: User-Specific Installation (Recommended for J-Link V7.70e and later)

Copy the entire `JLinkDevices` folder contents to the user-specific JLinkDevices directory:

#### Windows
```
%APPDATA%\SEGGER\JLinkDevices
```
Full path example: `C:\Users\<USERNAME>\AppData\Roaming\SEGGER\JLinkDevices`

#### Linux
```
$HOME/.config/SEGGER/JLinkDevices
```

#### macOS
```
$HOME/Library/Application Support/SEGGER/JLinkDevices
```

**Final directory structure should look like:**
```
JLinkDevices/
├── JLinkDevices.xml
└── Devices/
    └── QUECTEL/
        └── <DEVICE_NAME>/
```

### Method 2: Installation Directory Installation (For older versions or system-wide installation)

Copy the entire `JLinkDevices` folder contents directly to your J-Link installation directory:

#### Windows
```
C:\Program Files\SEGGER\JLink\JLinkDevices
```

#### Linux
```
/opt/SEGGER/JLink/JLinkDevices
```

#### macOS
```
/Applications/SEGGER/JLink/JLinkDevices
```

> **Note:** This method works for all J-Link versions and provides system-wide device support, but may require administrator/root privileges.

## Verification

After installation, you can verify the devices are recognized by:

1. **Using J-Link Commander:**
   ```
   JLink.exe
   > ?
   ```
   You should see `FCM363X`, `FCMA62N`, and `FGMH63X` in the device list.

2. **Using J-Flash:**
   - Open J-Flash
   - Go to Options → Project Settings → CPU
   - Search for "QUECTEL" or the specific device name

## Device Details

| Device | Interface | Device Identifier | Max Speed (kHz) |
|:------:|:---------:|:-----------------:|:---------------:|
| FCMA62N | SWD | RW610:RDRW610 / FCMA62N | 96000 |
| FCM363X | JTAG | FCM363X | 10000 / 15000* |
| FGMH63X | JTAG | FGMH63X | 10000 / 15000* |
| FCM363X-L | JTAG | RW610 | 10000 / 15000* |

\* 15000 kHz if supported by the debugger

## Files Included

- **JLinkDevices.xml** - Device database containing chip definitions
- **\*.FLM** - Flash loaders for programming external FLEXSPI flash memory
- **\*.JLinkScript** - Device-specific initialization and reset scripts

## Usage with IDEs

### MCUXpresso for VS Code

Configure `.vscode/launch.json` with the appropriate device name:

```json
"gdbServerConfigs": {
  "segger": {
    "device": "FCM363X",
    "interface": "JTAG",
    "speed": "10000"
  }
}
```

### Other IDEs

When configuring your debug session, select the appropriate device name from the device list.

## Technical Reference

For more information about the J-Link Device Support Kit, please refer to:
- [SEGGER J-Link Device Support Kit](https://kb.segger.com/J-Link_Device_Support_Kit)
- [SEGGER Flash Loader Documentation](https://kb.segger.com/SEGGER_Flash_Loader)
- [J-Link Script Files](https://kb.segger.com/J-Link_script_files)
