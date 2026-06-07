# LoRa Pump Control — Wireless Relay System

> **SKU:** P-0294 &nbsp;|&nbsp; **UI:** v2.1 &nbsp;|&nbsp; **Firmware:** RX-v3.6 &nbsp;|&nbsp; **Last Updated:** April 2026

A wireless remote relay system for switching and monitoring a **230 V AC pump load** from a Windows PC — with **no Wi-Fi or cellular network** required. A LoRa radio link connects a Local Transmitter (Tx) at your PC to a Remote Receiver (Rx) in the field.

---

## Table of Contents

- [System Overview](#system-overview)
- [Hardware Components](#hardware-components)
- [Safety](#safety)
- [Hardware Setup](#hardware-setup)
- [Software Installation](#software-installation)
- [Using the Control Software](#using-the-control-software)
- [Status Indicators Reference](#status-indicators-reference)
- [Battery Backup](#battery-backup)
- [Troubleshooting](#troubleshooting)
- [Technical Specifications](#technical-specifications)
- [License](#license)

---

## System Overview

```
[Windows PC] ──USB──► [Local Tx Device] ──LoRa Radio──► [Remote Rx Device] ──Relay──► [230V Pump]
```

| Component | Role | Connects To |
|---|---|---|
| **Local Device (Tx)** | Transmits commands from PC to field | PC via USB-A |
| **Remote Device (Rx)** | Receives commands, controls pump | 230V load + mains sense |
| **LoRa Control UI** | Windows desktop application | Tx device via COM port |

**Key Features:**
- Long-range wireless control with no Wi-Fi or cellular dependency
- 230V AC relay switching (5A rated, 2 Form C)
- Live RSSI/SNR signal monitoring with graphing
- Automated crop/irrigation scheduling (daily, day-of-week)
- Full event history with CSV/PDF/PNG export
- Li-Ion battery backup with automatic failover
- Remote diagnostics — test hardware without site visits

---

## Hardware Components

### Remote Device (Rx) — Top Panel

| Component | Location | Description |
|---|---|---|
| OLED Display | Top-center | Shows RSSI, SNR, relay state, and mains status in real time |
| PWR LED | Bottom-left (red) | Illuminates when the device has power |
| TX LED / RX LED | Above OLED | Blink on every wireless packet transmitted or received |
| PUMP STATUS LED | Next to pump block | White — illuminates when relay is energised (pump ON) |
| FLASHING LED | Bottom-left | Active only during a firmware update |
| BOOT button | Orange | Hold during reset to enter firmware flash mode |
| RESET button | Orange | Resets the microcontroller |
| USER button | Orange | User-configurable |
| PUMP Block | Top-left | 230V AC relay — switches pump load on command |

### Remote Device (Rx) — Right Panel (230V Connectors)

> ⚠️ **WARNING:** `230V SENSE` accepts a **low-voltage conditioned sense signal only** — NOT raw 230V mains. Use the purpose-built sense cable supplied with the unit.

| Connector | Description |
|---|---|
| **230V SENSE** *(left)* | Mains-sense input. Detects whether AC power is available at the remote site. |
| **LOAD** *(right)* | Relay-switched 230V AC output. Connect the pump or appliance here. |

### Local Device (Tx) — Side Panel

| Component | Description |
|---|---|
| Type-C Charging Port | Primary power input (5V). Connect to a 5A DC adapter. |
| Vin LED | Illuminates when input voltage is present |
| Charge LED | Red — battery is currently charging |
| Status LED (green) | Green — device operating normally |
| Vout LED (blue) | Blue — output voltage active, device communicating |
| Full LED | Battery is fully charged |
| Debug Port | Internal use only — do not connect |

---

## Safety

> ⛔ **DANGER:** This device interfaces with **230V AC mains electricity**. De-energise the circuit before making any wiring connections. Only qualified electricians should handle 230V wiring.

> ⚠️ **WARNING:** Never connect raw 230V AC wires to the `230V SENSE` port.

> ⚠️ **WARNING:** Always attach the SMA antenna **before** powering on. Operating without an antenna permanently damages the LoRa radio module.

| Rule | Detail |
|---|---|
| ✔ Relay rating | Verify relay current rating is sufficient for the connected load (5A @ 230VAC) |
| ✔ Battery type | Use only the compatible Li-Ion battery on the Remote device |
| ✔ Environment | Do not expose either device to moisture, excessive heat, or corrosive environments |
| ✔ Enclosure | Do not open the enclosure while connected to mains or USB power |
| ✔ Regulations | Ensure LoRa radio operation complies with local regulations (IN865) |

---

## Hardware Setup

### Remote Device (Rx)

1. **Attach the LoRa antenna** — connect the supplied antenna firmly to the SMA connector on the back panel. Do this **before** applying power. Do not remove.
2. **Connect the LOAD cable** — wire the pump/appliance to the LOAD terminal on the right panel. Use a qualified electrician.
3. **Connect the SENSE cable** — plug the purpose-built sense cable into the `230V SENSE` terminal.
4. **Apply USB-C power** — connect a 5V USB-C adapter. The OLED illuminates within a few seconds showing RSSI and SNR values.

> ℹ️ The device begins transmitting LoRa packets immediately after power-on. It is ready to receive commands as soon as the OLED shows values.

### Local Device (Tx)

1. Connect the Tx to your PC via USB-A.
2. The Status LED (red) should illuminate, confirming power and normal operation.

---

## Software Installation

1. **Locate the installer** — `LoRa Pump Controller Setup.exe` on your USB drive or downloads folder.
2. **Run the installer** — double-click. If Windows SmartScreen appears, click **More Info → Run Anyway**.
3. **Follow the setup wizard** — the app installs to Program Files and creates a desktop shortcut.
4. **Launch** — double-click the desktop shortcut.

> ℹ️ No internet connection is required. The installer is fully self-contained and can be transferred by USB drive.

**System Requirements:**
- Windows 10 / 11
- USB-A port
- ~50 MB disk space

---

## Using the Control Software

### Connecting (Dashboard)

On first launch, the status dot in the top navigation bar will be **RED** (disconnected).

1. Find the **SERIAL LINK** dropdown in the top-right area of the Dashboard.
2. Select the port labelled `USB Serial Port` (e.g. `COM29`). If unsure, check Windows **Device Manager → Ports**.
3. Click the green **CONNECT** button.
4. The status dot changes from **RED → GREEN**. The dashboard shows live data.

### Dashboard Tab

Once connected, the Dashboard is divided into three rows:

**Top Status Strip (6 Mini-Cards):**

| Card | What It Shows |
|---|---|
| PUMP STATUS | Green dot = ON / Red dot = OFF |
| REMOTE AC POWER | Whether mains electricity is available at the field site |
| BACKUP / SHUTDOWN | Battery backup health — NORMAL or alert state |
| ACTIVE CROP PLAN | Name of the currently active schedule (or "No Active Plan") |
| LINK EFFICIENCY | Wireless link quality as a percentage (100% = perfect) |
| SYSTEM MODE | LOCAL (manual control) or REMOTE (scheduled plan running) |

**Pump Control Card (Bottom-Left):**
- Click **PUMP ON** / **PUMP OFF** to manually control the pump
- The animated spinning gear shows Green (RUNNING) or dim/red (STOPPED)
- The yellow status bar confirms command state: `Transmitting → Confirmed`

**Hardware Link Quality Card (Bottom-Centre):**

| Value | Range | Colour | Meaning |
|---|---|---|---|
| RSSI | -30 to -60 dBm | Green | Excellent — ideal |
| RSSI | -60 to -90 dBm | Amber | Good — reliable |
| RSSI | -90 to -110 dBm | Amber/Red | Fair — consider repositioning |
| RSSI | Below -110 dBm | Red | Poor — check antenna |
| SNR | > 0 dB | Green | Clean signal |
| SNR | Near 0 dB | Amber | Some noise — monitor |

Click **VIEW GRAPH** to open a live scrolling chart of signal strength over time.

**Power Status Card (Bottom-Right):**
- **AC MAINS** — Green "STABLE" = mains present; Red "AC LOST" = power failure
- **BACKUP UPS** — "Standby" = battery healthy; "Active" = running on battery
- A red timer counts up automatically when AC power is lost
- Click **QUERY NOW** for an immediate status refresh

### Pump Controller Tab

Provides detailed manual control and automated crop scheduling.

**Pump State LEDs (mirror physical hardware LEDs):**

| LED Colour | State | Meaning |
|---|---|---|
| ● Blue | ON | System in scheduled/automatic mode |
| ● Green | ON | Pump is running |
| ● Red | ON | Pump is stopped |
| ● Blue + Green | Both ON | Scheduled automation running |
| ● Blue + Red | Both ON | Scheduled automation stopped |

**Crop Scheduler:**
1. Select **Crop Name** — Wheat, Corn, Rice, or Custom
2. Set **Duration (Minutes)** — how long the pump runs per session
3. Set **Start Time** — the Stop Time is calculated automatically (Start + Duration)
4. Select **Active Days** — click Su/Mo/Tu/We/Th/Fr/Sa to toggle
5. Click **Save Plan** — the schedule is saved and runs automatically

> ℹ️ The LoRa Control UI must be **running** on your PC at the scheduled time. It does not run in the background when closed.

**Command Log:** A live table at the bottom records each action with timestamp and ACK status.

### Diagnostics Tab

Remotely test individual hardware components on the Rx device without visiting the field.

| Test | What It Does |
|---|---|
| Ping Test | Round-trip health check, measures response time in ms |
| Relay Click | Cycles relay ON then OFF — you hear a physical "click" |
| Buzzer Test | 500ms beep on the Rx buzzer |
| LED Sweep | Cycles Red → Green → Blue LEDs on the Rx device |
| OLED Message | Sends a test pattern to the OLED display |
| AC Query | Reads the mains sense pin |
| Shutdown Sense | Reads the UPS sense pin — confirms battery backup health |

Click **Run Full Self-Test** to run all 7 tests sequentially.

The scrolling console shows raw timestamped packets with **PASS** (green) or **TIMEOUT/FAIL** (red) per test.

### History & Logs Tab

Permanent, chronological log of every system event. Survives application restarts.

**Event Status Colours:**

| Status | Colour | Meaning |
|---|---|---|
| SENT | White | Command sent to remote device |
| ACK | Green | Remote device acknowledged |
| CONFIRMED | Green | Remote device confirmed action completed |
| ALARM | Red/Orange | Critical event (e.g. AC power lost) |
| STABLE | Green | Previously alarmed condition returned to normal |

**Export Options:**
- Export as **Image (PNG)**
- Export as **CSV**
- Export as **PDF Report**

**View Modes:** Table view or 24-hour Gantt Chart timeline view.

> ⚠️ **WARNING:** Clear History is permanent and cannot be undone. Export logs before clearing.

---

## Status Indicators Reference

### UI Status Dot

| Colour | Meaning | Action |
|---|---|---|
| ● Green | Connected — system online | Normal operation |
| ● Red | Disconnected — no COM port link | Select correct COM port and click Connect |

### Remote Device — Relay Status LEDs

| LED Combination | Meaning |
|---|---|
| Green only | Relay energised — pump running |
| Red only | Relay off — pump stopped |
| Blue + Green | Scheduled automation active and running |
| Blue + Red | Scheduled automation ended |
| Red flashing | Critical battery warning — very low battery |

### Remote Device — UPS LED Reference

| LED | Colour | Meaning |
|---|---|---|
| Vin LED | Red/On | Input power present |
| Charge LED | Red | Battery is charging |
| Status LED | Green | Device operating normally |
| Vout LED | Blue | Output voltage active — device communicating |
| Full LED | Blue/White | Battery is fully charged |

---

## Battery Backup

The Remote Device includes a Li-Ion battery backup for mains power outages.

| Feature | Detail |
|---|---|
| Automatic switchover | Instantly switches to battery when mains/USB lost — no interruption |
| Full functionality | Relay control, wireless comms, OLED, and LEDs all remain active on battery |
| Auto-recharge | Battery recharges automatically when external power returns |
| Charging port | Use the Type-C Charging port with a 5V DC adapter |

> ⚠️ **CAUTION:** If the device powers off immediately when USB is disconnected, the battery may be discharged or not connected. Charge via the Type-C Charging port.

---

## Troubleshooting

| Symptom | Suggested Action |
|---|---|
| OLED display does not light up | Check USB cable is firmly connected. Try a different cable/port. If on battery, charge via Type-C Charging port. |
| Software shows OFFLINE / red status dot | Verify correct COM port is selected. Disconnect and reconnect USB, then refresh the COM port dropdown. |
| Relay does not respond to commands | Check signal quality (RSSI should be above -110 dBm). Verify antenna is attached and Rx device is powered on. |
| 230V SENSE always shows NOT AVAILABLE | Check sense cable connection. Verify the monitored circuit has power and is switched on. |
| Device powers off when USB removed | Battery is discharged or not connected. Charge via the Type-C Charging port. |
| Scheduled automation does not start | Verify the plan was saved. Confirm correct days are selected. Ensure LoRa Control UI is open at the scheduled time. |
| Signal quality shows Poor (Red) | Reposition device to reduce obstacles. Verify antenna is secure. Move away from interference sources (Wi-Fi routers, metal surfaces, microwave ovens). |

---

## Technical Specifications

| Specification | Detail |
|---|---|
| Wireless Technology | LoRa long-range radio |
| Radio Frequency | IN865 |
| SKU | P-0294 |
| Power Input | USB-C, 5V DC |
| Battery Backup | Li-Ion — automatic failover |
| Relay Output | Normally Open (N/O), 230V AC rated |
| Relay Current Rating | 5A @ 230VAC / 28V DC (2 Form C) |
| 230V Sense Input | Low-voltage conditioned input (NOT raw mains) |
| Status Indicators | RGB LEDs + OLED display |
| PC Communication | USB-Serial virtual COM port (Windows) |
| Control Software | LoRa Control UI v2.1 — Windows desktop application |
| Firmware Version | RX-v3.6 |
| Enclosure | 3D-printed polymer, black |

### Power Consumption

| Device | Condition | Current Draw |
|---|---|---|
| Local Device (Tx) | Transmitting | 0.07 A |
| Local Device (Tx) | Connected / idle | 0.06 A |
| Remote Device (Rx) | Working / relay active | ~0.25 A |
| Remote Device (Rx) | Idle | 0.020 A |

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

*SKU P-0294 | UI v2.1 | FW RX-v3.6 | April 2026*
