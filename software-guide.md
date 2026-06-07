# Software Guide — LoRa Control UI v2.1

## Installation

1. Locate `LoRa Pump Controller Setup.exe` on your USB drive or downloads folder
2. Double-click to run the installer
3. If Windows SmartScreen appears: click **More Info → Run Anyway**
4. Follow the setup wizard — the app installs to Program Files and creates a desktop shortcut
5. Launch by double-clicking the desktop shortcut

**Requirements:**
- Windows 10 or Windows 11
- USB-A port available
- Approximately 50 MB disk space
- No internet connection required

---

## Application Layout

The application has four main tabs accessible from the top navigation bar:

| Tab | Purpose |
|---|---|
| **Dashboard** | Main overview and quick pump control |
| **Pump Controller** | Detailed control + crop scheduling |
| **Diagnostics** | Remote hardware testing |
| **History & Logs** | Permanent event log and export |

---

## Connecting to the Device

The status dot in the top navigation bar indicates connection state:
- 🔴 **Red** = disconnected
- 🟢 **Green** = connected

**To connect:**
1. Find the **SERIAL LINK** dropdown in the top-right of the Dashboard
2. Select `USB Serial Port (COM##)` — if unsure, check Device Manager → Ports
3. Click the green **CONNECT** button
4. Status dot changes to Green; live data populates the dashboard

---

## Dashboard Tab

### Top Status Strip

Six quick-glance mini-cards show the full system state:

| Card | Indicators |
|---|---|
| **PUMP STATUS** | 🟢 Green = ON / 🔴 Red = OFF |
| **REMOTE AC POWER** | STABLE / AC LOST |
| **BACKUP / SHUTDOWN** | NORMAL / alert state |
| **ACTIVE CROP PLAN** | Plan name or "No Active Plan" |
| **LINK EFFICIENCY** | % (100% = perfect signal) |
| **SYSTEM MODE** | LOCAL / REMOTE |

### Pump Control Card (Bottom-Left)

| Action | Result |
|---|---|
| Click **PUMP ON** | Sends ON command; wait 1–3 s for confirmation |
| Click **PUMP OFF** | Sends OFF command; status bar shows "Confirmed: PUMP OFF" |

The animated spinning gear shows the pump state:
- 🟢 Green spinning = RUNNING
- 🔴 Red/dim = STOPPED

### Hardware Link Quality Card (Bottom-Centre)

Displays live RSSI and SNR for both Tx (local) and Rx (remote) units.

| RSSI Range | Quality |
|---|---|
| -30 to -60 dBm | 🟢 Excellent |
| -60 to -90 dBm | 🟡 Good |
| -90 to -110 dBm | 🟠 Fair |
| Below -110 dBm | 🔴 Poor |

Click **VIEW GRAPH** to open a live scrolling RSSI/SNR chart.

### Power Status Card (Bottom-Right)

| Indicator | Meaning |
|---|---|
| AC MAINS — "STABLE" (green) | Mains power present at field site |
| AC MAINS — "AC LOST" (red) | Mains power failure detected |
| BACKUP UPS — "Standby" | Battery healthy, on standby |
| BACKUP UPS — "Active" | Running on battery backup |

When AC is lost, a red timer automatically counts up showing outage duration.  
Click **QUERY NOW** to force an immediate status refresh.

---

## Pump Controller Tab

### Pump State LEDs

These mirror the physical LEDs on the remote hardware:

| LED | Meaning |
|---|---|
| 🔵 Blue | Scheduled/automatic mode active |
| 🟢 Green | Pump is running |
| 🔴 Red | Pump is stopped |
| 🔵🟢 Blue + Green | Schedule running |
| 🔵🔴 Blue + Red | Schedule stopped |

### Crop Scheduler

Set up automated irrigation schedules:

1. **Select Crop Name** — choose Wheat, Corn, Rice, or Custom (type your own name)
2. **Set Duration (Minutes)** — runtime per session (e.g. 60 = one hour)
3. **Set Start Time** — when the pump should turn ON each day
   - Stop Time is calculated automatically: Start Time + Duration
4. **Select Active Days** — click Su / Mo / Tu / We / Th / Fr / Sa to toggle
   - Active days appear highlighted
5. **Click Save Plan** — schedule is saved and will fire automatically

> ⚠️ **Important:** The LoRa Control UI must be **open and running** on your PC at the scheduled time. The app does not run in the background when closed.

### Command Log

A live table at the bottom of the tab records:
- Serial number
- Timestamp
- Action sent (e.g. "Pump Turned OFF")
- Status (ACK = acknowledged by remote device)

---

## Diagnostics Tab

Run remote hardware tests without visiting the field site.

### Individual Tests

| Test | What Happens |
|---|---|
| **Ping Test** | Round-trip health check — measures response time in ms |
| **Relay Click** | Cycles relay ON then OFF — audible "click" at remote device |
| **Buzzer Test** | 500ms beep on Rx buzzer |
| **LED Sweep** | Red → Green → Blue LED cycle on Rx device |
| **OLED Message** | Sends test pattern to Rx OLED display |
| **AC Query** | Reads mains sense pin — confirms AC power detection |
| **Shutdown Sense** | Reads UPS sense pin — confirms battery backup health |

Click **Run Full Self-Test** to run all 7 tests in sequence automatically.

### Test Output Console

The scrolling terminal shows:
- Timestamped raw packets (sent and received)
- **PASS** ✅ (green) or **TIMEOUT / FAIL** ❌ (red) per test

---

## History & Logs Tab

Permanent record of all system events, saved to your PC's hard drive.

### Event Table Columns

| Column | Description |
|---|---|
| Time | Timestamp of the event |
| Category | AC / PUMP / CMD |
| Event | Description of what happened |
| Status | SENT / ACK / CONFIRMED / ALARM / STABLE |

### Status Colour Codes

| Status | Colour | Meaning |
|---|---|---|
| SENT | White | Command sent |
| ACK | Green | Remote device acknowledged |
| CONFIRMED | Green | Action completed on remote device |
| ALARM | Red/Orange | Critical event (e.g. AC power lost) |
| STABLE | Green | Alarmed condition resolved |

### Export & View Controls

| Control | Function |
|---|---|
| **Export as Image** | Saves log table as PNG |
| **Export as CSV** | Saves raw data as spreadsheet-compatible CSV |
| **Export as PDF Report** | Saves formatted PDF report |
| **View Mode** | Toggle between Table and 24-hour Gantt Chart |
| **Back to Table** | Returns from Gantt chart view |
| **Clear History** | Permanently deletes all log data |

> ⚠️ **Clear History is permanent.** Export your logs before clearing.

---

*For hardware setup, see [Hardware Setup Guide](hardware-setup.md)*  
*For troubleshooting, see the [Troubleshooting section in README](../README.md#troubleshooting)*
