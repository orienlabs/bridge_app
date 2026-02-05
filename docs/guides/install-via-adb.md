# Install Bridge without Google Play (ADB / Sideload) 🔧

**Summary:** This guide shows how to install the Bridge app without Play Store using ADB or by sideloading with a File Browser app. Installing the File Browser first is recommended because it makes future updates easy (no ADB needed).

---

## Important downloads

- Bridge APK: https://olabs.app/resources/bridge.apk
- File Browser APK (recommended): https://olabs.app/resources/file-browser.apk

> Tip: Only install APKs from trusted sources.

---

## Before you start ✅

- Make sure your Wear OS watch is paired for wireless ADB — pairing steps vary by device, so search for "set up ADB for Wear OS" or your watch model.
- This guide does not walk through pairing ADB; follow a device-specific tutorial for pairing and authorizing ADB.
- Once paired, confirm the connection with:

```bash
adb devices
```

You should see your watch listed. If it shows `unauthorized`, accept the prompt on the watch.

---

## Recommended (easiest): Install File Browser first and use it to install Bridge 📁

Why? If you install the File Browser and grant it permission to install unknown apps, you can download future Bridge APKs directly on the device and install them without connecting via ADB.

### Steps

1. Install the File Browser APK on your watch. After you pair the watch for wireless ADB you can install it from your computer with:

```bash
adb install -r -g file-browser.apk
```

2. Ensure your phone and watch are connected to the same Wi‑Fi network. In File Browser on the watch start the web service — the app will show a QR code (and a URL).

3. On your phone, scan the QR code (or visit the URL) to open the File Browser web UI in your phone's browser. In the web UI upload the `bridge.apk` to the Files section, then choose to install it from the browser (3 dot menu for uploaded file). 

4. Finish installation steps on the watch. This installs the APK on the watch without any further ADB connection.

5. After installation, future updates are easy: upload the new `bridge.apk` to the File Browser web UI and install from the phone browser.

**Note:** If Bridge is already installed from Google Play, uninstall the Play Store version first to avoid signature conflicts.

---

## Direct install via ADB (no File Browser) ⌨️

1. Ensure your watch is paired for wireless ADB and visible via `adb devices`. If multiple devices are listed, use the device serial with `-s` (examples below).

2. Install (or update) via ADB from your computer — `adb install` sends the APK directly to the device (no separate push required):

```bash
adb install -r -g bridge.apk
# If multiple adb devices are connected:
adb -s <serial> install -r -g bridge.apk
```

- Use `-r` to replace an existing app (keep data).
- Use `-g` to grant runtime permissions.
- To allow downgrades: `adb install -r -d bridge.apk`.

3. Verify install by opening Bridge on the watch.

**If you get an error** like `INSTALL_FAILED_UPDATE_INCOMPATIBLE`, that usually means the signatures differ. Uninstall the existing app (Play Store or other) first and try again.

---

## Troubleshooting ⚠️

- `adb devices` shows `unauthorized`: Accept the RSA prompt on the watch and re-run `adb devices`.
- Multiple devices listed: if `adb devices` shows more than one entry, use the watch serial with `-s`: `adb -s <serial> install -r -g bridge.apk`. Use `adb devices -l` to get more details.
- `INSTALL_FAILED_UPDATE_INCOMPATIBLE` or "App not installed": that usually means signatures differ. Uninstall the conflicting app (Play Store version or another build) first and try again.

---

## Helpful commands (examples)

```bash
# Check devices
adb devices

# Install APK (replace existing, grant permissions)
adb install -r -g bridge.apk

# If multiple devices are connected, install using serial:
adb -s <serial> install -r -g bridge.apk
```

---

## Security & notes 🔒

- Only install APKs you trust.
- If installing from Play Store and then sideloading, uninstall the Play Store version first to avoid signature mismatch.
- Keep backups if you're concerned about preserving app data.

---
