# Changelog

All notable changes to this project will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [v2.1 / RX-v3.6] — April 2026

### Added
- Crop Scheduler with day-of-week selection (Su/Mo/Tu/We/Th/Fr/Sa)
- Custom crop name field alongside presets (Wheat, Corn, Rice)
- 24-hour Gantt Chart timeline view in History & Logs tab
- Export options: PNG image, CSV, and PDF Report
- Run Full Self-Test button (runs all 7 diagnostic tests sequentially)
- Live scrolling RSSI/SNR graph (VIEW GRAPH button on Dashboard)
- Red outage timer — counts up automatically when AC power is lost
- QUERY NOW button for forced remote status refresh

### Changed
- Dashboard reorganised into three-row layout with 6 top mini-cards
- RSSI colour thresholds refined (Green / Amber / Red bands)
- Status bar now shows `Transmitting → Confirmed` transition for pump commands

### Fixed
- COM port dropdown now refreshes correctly after USB reconnect
- Scheduled plan stop time calculation corrected (Start + Duration)

---

## [v2.0 / RX-v3.x] — Earlier

- Initial public release with Dashboard, Pump Controller, Diagnostics, and History tabs
- Basic LoRa Tx/Rx relay control over USB-Serial COM port
- Li-Ion battery backup with automatic failover
- OLED display showing RSSI, SNR, relay state, and mains status
