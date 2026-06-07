# Technical Specifications — LoRa Pump Control (SKU: P-0294)

## System Specifications

| Specification | Detail |
|---|---|
| SKU | P-0294 |
| Control Software | LoRa Control UI v2.1 |
| Firmware Version | RX-v3.6 |
| Wireless Technology | LoRa long-range radio |
| Radio Frequency Band | IN865 (India 865–867 MHz) |
| PC Communication | USB-Serial virtual COM port (Windows) |
| Enclosure | 3D-printed polymer, black |

---

## Relay Specifications

| Parameter | Value |
|---|---|
| Relay Type | 2 Form C (DPDT) |
| Rated Switching Voltage | 230V AC / 28V DC |
| Rated Switching Current | 5A |
| Contact Configuration | Normally Open (N/O) |

---

## Power Specifications

| Parameter | Value |
|---|---|
| Power Input | USB-C, 5V DC |
| Recommended Adapter | 5V, 5A DC adapter |
| Battery Backup | Li-Ion, automatic failover |
| Battery Charging | Via Type-C Charging port, 5V DC |

### Power Consumption

| Device | Condition | Current Draw |
|---|---|---|
| Local Device (Tx) | Transmitting | 0.07 A |
| Local Device (Tx) | Connected / idle | 0.06 A |
| Remote Device (Rx) | Working / relay active | ~0.25 A |
| Remote Device (Rx) | Idle | 0.020 A |

---

## Signal Quality Reference

| RSSI Range | SNR | Quality | Action |
|---|---|---|---|
| -30 to -60 dBm | > 0 dB | 🟢 Excellent | No action needed |
| -60 to -90 dBm | > 0 dB | 🟡 Good | Monitor |
| -90 to -110 dBm | Near 0 dB | 🟠 Fair | Consider repositioning |
| Below -110 dBm | Any | 🔴 Poor | Reposition, check antenna |

---

## Connectors & Interfaces

### Remote Device (Rx)

| Connector | Location | Purpose |
|---|---|---|
| SMA Antenna Port | Back panel | LoRa antenna connection — attach before power-on |
| 230V SENSE | Right panel (left) | Low-voltage mains sense input |
| LOAD | Right panel (right) | Relay-switched 230V AC output |
| Type-C Charging Port | Front panel | 5V power input / battery charging |
| USB Flashing Port | Front panel | Firmware development only — do not use |

### Local Device (Tx)

| Connector | Location | Purpose |
|---|---|---|
| USB-A | Side panel | PC connection (COM port) |
| Type-C Charging Port | Side panel | 5V power input |
| Debug Port | Side | Firmware use only — do not use |

---

## Indicators

### Remote Device (Rx) LEDs

| LED | Colour | Meaning |
|---|---|---|
| PWR | Red | Device has power |
| TX | Blinks | Wireless packet transmitted |
| RX | Blinks | Wireless packet received |
| PUMP STATUS | White | Relay energised (pump ON) |
| FLASHING | — | Firmware update in progress |

### Relay Status LEDs

| Combination | Meaning |
|---|---|
| Green only | Relay ON — pump running |
| Red only | Relay OFF — pump stopped |
| Blue + Green | Scheduled automation — running |
| Blue + Red | Scheduled automation — stopped |
| Red flashing | Critical battery warning |

### UPS / TinyUPS LEDs

| LED | Colour | Meaning |
|---|---|---|
| Vin | Red / On | Input power present |
| Charge | Red | Battery charging |
| Status | Green | Normal operation |
| Vout | Blue | Output voltage active |
| Full | Blue / White | Battery fully charged |

---

## Regulatory

| Parameter | Detail |
|---|---|
| Radio Band | IN865 (India LoRa band, 865–867 MHz) |
| Regulatory Compliance | Ensure operation complies with local LoRa regulations |

---

## Software Environment

| Parameter | Detail |
|---|---|
| Supported OS | Windows 10, Windows 11 |
| Driver | USB-Serial (installs automatically) |
| Installation | Self-contained installer, no internet required |
| Scheduler | PC clock-based; UI must be running for automation |
| Log Storage | Local PC hard drive, persistent across restarts |
| Export Formats | PNG, CSV, PDF |
