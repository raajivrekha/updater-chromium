# updater-chromium
This is a practical, self-validating bash utility for macOS that keeps the Chromium browser (not Chrome) updated to the latest snapshot. It is designed to be a "set-and-forget" tool that lives in your system path and runs a check every morning (10:00AM)

## # What it does
This script is designed to be a "set-and-forget" tool that keeps your Chromium build fresh without manual downloads or security prompt headaches.

* **Self-Provisioning:** On the first run, it mirrors itself to `/usr/local/bin` so you can run `updater-chromium` from any terminal window.
* **Daily Automation:** It registers a macOS LaunchAgent to check for updates every morning at **10:00 AM**.
* **Bandwidth Efficient:** It performs a header-only "ETag" check. If the online version matches your local version, it exits in under a second without downloading the 100MB+ Chromium latest snapshot/archive.
* **Atomic Deployment:** If an update is found, it kills active Chromium processes, swaps the app bundle in `/Applications`, and strips the macOS "Quarantine" flag so the app opens immediately.
* **Integrity Checks:** It lints its own XML syntax via `plutil` and runs a headless smoke test (`--version`) on every new download to ensure the binary isn't corrupted.

---

## # Installation & Usage

### 1. Initial Setup
Run the script from your downloads or scripts folder. It will handle the pivot to your system path and schedule the daily task automatically.
```bash
chmod +x updater-chromium
./updater-chromium
