# docs/Hardware Setup Guide

> ⛔ **DANGER:** This device interfaces with 230V AC mains electricity. De-energise the circuit before making any wiring connections. Only qualified electricians should handle 230V wiring.

---

## What's in the Box

- Remote Device (Rx) — field unit with relay and OLED
- Local Device (Tx) — PC-connected unit
- LoRa antenna (SMA connector) × 2
- Purpose-built 230V SENSE cable
- USB-A cable (Tx to PC)
- USB-C cable (Rx power)

---

## Step 1 — Prepare the Remote Device (Rx)

### 1.1 Attach the Antenna

Connect the supplied LoRa antenna to the SMA connector on the **back panel** of the Rx device.

> ⚠️ **Do this BEFORE applying any power.** Operating without an antenna permanently damages the LoRa radio module. Do not remove the antenna once attached.

### 1.2 Wire the LOAD Output

Wire the pump or appliance to the **LOAD terminal** on the right panel. This is the relay-switched 230V AC output.

- Use a qualified electrician for all 230V wiring
- Verify the relay rating (5A @ 230VAC) is sufficient for your load before wiring
- Use appropriate cable gauge for the current draw

### 1.3 Connect the SENSE Cable

Plug the purpose-built sense cable into the **230V SENSE terminal** on the right panel (the left connector on the right panel).

> ⚠️ **WARNING:** Do NOT connect raw 230V mains wires to the SENSE port. It accepts a low-voltage conditioned signal from the supplied sense cable only.

### 1.4 Apply USB-C Power

Connect a 5V USB-C adapter to the Type-C Charging port on the Rx device.

**Expected on power-up:**
- PWR LED (red) illuminates
- OLED lights up within a few seconds
- OLED shows RSSI and SNR values
- TX/RX LEDs blink as packets are transmitted

> ℹ️ The device begins transmitting LoRa packets immediately. It is ready to receive commands as soon as the OLED shows values.

---

## Step 2 — Set Up the Local Device (Tx)

1. Connect the Tx device to your PC using the USB-A cable.
2. Windows will install drivers automatically (USB-Serial virtual COM port).
3. Check that the **Status LED (red)** illuminates on the Tx device.
4. Open **Windows Device Manager → Ports** to confirm the COM port number (e.g. `COM29`).

---

## Step 3 — Verify Connection

With both devices powered:

1. The Rx OLED should show live RSSI and SNR values — these are the signal readings from the Tx.
2. Typical RSSI at short range: -30 to -60 dBm (Green/Excellent)
3. The TX and RX LEDs on both devices should blink periodically

---

## Panel Reference Diagrams

### Rx Device — Right Panel (230V Side)

```
┌─────────────────────────┐
│  [230V SENSE]  [LOAD]   │  ← Right panel, viewed from outside
│  (mains sense) (relay   │
│                 output) │
└─────────────────────────┘
```

### Rx Device — Top Panel

```
┌─────────────────────────────────────────┐
│  [PUMP Block]    [TX LED] [RX LED]      │
│  (230V relay)    [   OLED DISPLAY   ]   │
│  [PWR LED]       [BOOT] [RESET] [USER]  │
│  [FLASHING LED]  [PUMP STATUS LED]      │
└─────────────────────────────────────────┘
```

---

## Antenna Positioning Tips

- Mount antennas vertically (upright) for best omnidirectional coverage
- Avoid placing the Rx antenna directly against metal surfaces
- Keep away from Wi-Fi routers, microwave ovens, and other RF sources
- If RSSI is below -90 dBm, try repositioning for better line-of-sight

---

## Relay Specifications

| Parameter | Value |
|---|---|
| Type | 2 Form C (DPDT) |
| Rated Voltage | 230V AC / 28V DC |
| Rated Current | 5A |
| Configuration | Normally Open (N/O) |

---

*For software setup, see [Software Guide](software-guide.md)*
