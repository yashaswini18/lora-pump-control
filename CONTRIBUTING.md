# Contributing to LoRa Pump Control

Thank you for your interest in contributing! Here's how to get involved.

## Ways to Contribute

- **Bug reports** — open an Issue describing the problem, steps to reproduce, and expected vs actual behaviour
- **Feature requests** — open an Issue with the `enhancement` label describing the use case
- **Documentation** — fix typos, improve explanations, add missing details
- **Firmware / Software improvements** — submit a Pull Request (see below)

## Reporting Bugs

Please include:
- Your OS version (Windows 10 / 11)
- UI version (shown in app title bar)
- Firmware version (shown on dashboard)
- COM port and device details
- Steps to reproduce the issue
- What you expected vs what happened
- Any relevant logs from the History & Logs tab (export as CSV if possible)

## Pull Request Process

1. Fork the repository and create a branch: `git checkout -b feature/your-feature-name`
2. Make your changes with clear, descriptive commits
3. Test your changes thoroughly (run the full self-test via the Diagnostics tab if hardware-related)
4. Update documentation (README or relevant docs) if your change affects usage
5. Open a Pull Request with a clear description of what changed and why

## Code Style

- Keep commits focused — one logical change per commit
- Write clear commit messages: `fix: relay timeout not resetting after reconnect`
- Comment non-obvious hardware-specific behaviour

## Safety Notice

This project interfaces with **230V AC mains electricity**. Any contributions involving relay control, sense circuitry, or power handling must clearly document safety implications and must not lower the safety bar of the existing design.

## Questions?

Open a Discussion or an Issue — we're happy to help.
