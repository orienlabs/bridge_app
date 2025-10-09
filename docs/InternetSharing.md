# Internet Sharing Setup Guide

This guide explains how to grant the necessary system permissions to enable proxy functionality in the Bridge Wear OS app.

## TL;DR - Quick Permission Grant

To enable internet sharing, grant the app this permission via ADB:

```bash
adb shell pm grant com.orienlabs.bridge.wear android.permission.WRITE_SECURE_SETTINGS
```

Then restart the app.

**Why?** The `WRITE_SECURE_SETTINGS` permission allows the app to configure system proxy settings so your watch can route internet traffic through your connected iPhone. This is a protected Android permission that can only be granted via ADB.

**Limitation:** Max speed is ~64KB/s due to Bluetooth. Best for light browsing and notifications—not for downloading apps.

---

## Overview

The Bridge app requires special system-level permissions to control HTTP proxy settings on your Android Watch. These permissions cannot be granted through the normal Android permission system and must be set up via ADB (Android Debug Bridge).

## !Caution!

Max speed using this setup is 64KB/s which is a technical limitations. While this is good for day to day browsing, it is recommanded to be not used for internet heavy tasks such as app downloads. Good use case includes examples such as automated whether updates.

## Prerequisites

Before proceeding, ensure you have:

1. **Developer Options enabled** on your Android Watch
2. **Wireless debugging enabled** on your Android Watch
3. **ADB installed** on your computer
4. **Computer and Android Watch on the same Wi-Fi network**

## Required Permission

The app needs the `WRITE_SECURE_SETTINGS` permission to:
- Set system-wide HTTP proxy settings
- Clear system-wide HTTP proxy settings
- Enable/disable proxy functionality from within the app

## Step-by-Step Setup

### 1. Enable Developer Options on Wear OS

1. Open **Settings** on your Android Watch
2. Scroll down and tap **System**
3. Tap **About**
4. Tap **Build number** 7 times rapidly
5. You'll see "You are now a developer!" message

### 2. Enable Wireless Debugging

1. Go back to **Settings** → **System**
2. Tap **Developer options** (should now be visible)
3. Toggle **Wireless debugging** to ON
4. Tap **Pair New Device** display pairing code,
5. Note the **IP address and port** (e.g., `192.168.1.100:5555`)
6. Note the **6-digit pairing code**

### 3. Connect Your Device

1. On your computer, run the pairing command:
   ```bash
   adb pair <IP_ADDRESS_AND_PORT>
   ```
   Example:
   ```bash
   adb pair 192.168.1.100:5555
   ```
2. When prompted, enter the **6-digit pairing code**
3. After successful pairing, connect to the device (sometime, port can change, use currently displayed port):
   ```bash
   adb connect <IP_ADDRESS_AND_PORT>
   ```
   Example:
   ```bash
   adb connect 192.168.1.100:5555
   ```
4. Verify connection:
   ```bash
   adb devices
   ```
   You should see your device listed as `192.168.1.100:5555 device`

### 4. Grant the Permission

Run this command **once** on your computer:

```bash
adb shell pm grant com.orienlabs.bridge.wear android.permission.WRITE_SECURE_SETTINGS
```

**Expected output:**
```
# No output means success
```

### 5. Verify Permission

You can verify the permission was granted by running:

```bash
adb shell dumpsys package com.orienlabs.bridge.wear | grep WRITE_SECURE_SETTINGS
```

Look for:
```
android.permission.WRITE_SECURE_SETTINGS: granted=true
```

### 6. Restart the App

1. Force close the Bridge app on your Android Watch
2. Reopen the Bridge app
3. Go to **Advanced** >> **Internet Sharing** settings
4. You should now see control options available

## Important Notes for Wear OS

- **Wireless debugging is the only reliable method** for Android Watchs
- **Both devices must be on the same Wi-Fi network**
- **Pairing is required** - you cannot use the older `adb tcpip` method
- **Connection may drop** - you may need to reconnect if the device goes to sleep
- **IP address/ port may change** - if your device gets a new IP, you'll need to reconnect

## Using Proxy Controls

Once permissions are granted, bridge app will automatically set and reset proxy settings as needed. You do not have to set proxy manually. 

## Troubleshooting

### Permission Denied Error
```
SecurityException: Permission denied: writing to settings requires: android.permission.WRITE_SECURE_SETTINGS
```

**Solution:** The permission wasn't granted properly. Repeat step 4.

### Device Not Found
```
error: device not found
```

**Solutions:**
- Ensure wireless debugging is enabled and paired
- Check ADB connection: `adb devices`
- Try reconnecting: `adb connect <IP>:5555`
- Verify both devices are on the same Wi-Fi network

### Permission Not Persisting
If the permission disappears after app updates:

1. Re-grant the permission:
   ```bash
   adb shell pm grant com.orienlabs.bridge.wear android.permission.WRITE_SECURE_SETTINGS
   ```
2. Restart the app

### ADB Command Not Found
If `adb` command is not recognized:

1. **Install Android SDK Platform Tools**:
   - Download from [Android Developer website](https://developer.android.com/studio/releases/platform-tools)
   - Add to your system PATH

2. **Alternative**: Use Android Studio's built-in ADB:
   ```bash
   # On macOS/Linux
   ~/Library/Android/sdk/platform-tools/adb shell pm grant com.orienlabs.bridge.wear android.permission.WRITE_SECURE_SETTINGS
   
   # On Windows
   %LOCALAPPDATA%\Android\Sdk\platform-tools\adb.exe shell pm grant com.orienlabs.bridge.wear android.permission.WRITE_SECURE_SETTINGS
   ```

## Security Considerations

### Why This Permission is Required
- `WRITE_SECURE_SETTINGS` is a **signature-level** permission
- It allows modification of system-wide settings
- Normal apps cannot request this permission through standard means
- It's protected to prevent malicious apps from changing system settings

### Safety
- This permission allows the app to modify HTTP proxy settings. This is needed so that Bridge app can set itself to intercept network request and forward to connected iOS devices and relay responses back,
- It cannot access personal data or other sensitive settings
- The permission is granted specifically to our app package only

## Support

Please reach out to developers at bridge@olabs.app or on Reddit > r/orienlabs

## Summary

The permission setup is a **one-time process** that enables convenient proxy control from within the Bridge app. Once granted, it can easily enable/disable the proxy and switch between routing modes without needing ADB commands again.