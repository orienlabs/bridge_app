
# Capturing Battery Information to Identify Root Cause of Battery Drain

If you experience excessive battery drain while using the app, it is useful to capture battery information while the device discharges. This data can help identify the root cause and guide an appropriate fix.

This process requires **ADB tools** and assumes you already know how to connect your device to ADB.

---

### **Steps to Capture Battery Information**

1. **Charge your watch to 100%**
   - Start with a full charge to ensure accurate discharge tracking.

2. **Disconnect Charging**
   - Battery stats are only reliable when the device is discharging, not charging.

3. **Reset Battery Stats**
   - Before starting the test, clear previous stats:
     ```bash
     adb shell dumpsys batterystats --reset
     ```

4. **Enable Full Wake History (Optional but Recommended)**
   - This provides detailed wake lock information:
     ```bash
     adb shell dumpsys batterystats --enable full-wake-history
     ```

5. **Mark Device as Charged (Optional)**
   - Use `--charged` to indicate the device started at full charge. This helps normalize stats:
     ```bash
     adb shell dumpsys batterystats --charged
     ```

6. **Use the Device Normally**
   - Run the app and perform typical usage for several hours or until noticeable drain occurs.

7. **Capture Battery Stats**
   - **Full Stats**:
     ```bash
     adb shell dumpsys batterystats > batterystats_full.txt
     ```
   - **Stats for Your App Only**:
     ```bash
     adb shell dumpsys batterystats com.orienlabs.bridge.wear > batterystats_bridge.txt
     ```

8. **Optional: Generate a Bugreport**
   - For more comprehensive analysis:
     ```bash
     adb bugreport > bugreport.zip
     ```

---

### **Analyzing the Data**
- Look for:
  - **High CPU usage** by specific apps.
  - **Wake locks** that prevent the device from sleeping.
  - **Network activity** or frequent syncs.
  - **Sensor usage** (GPS, Bluetooth, etc.).

You can either use any AI tool available at your disposal to analyze. Use prompt given below as suggestion
```
Analyze the following Android battery stats to identify the root cause of battery drain. Focus on:
- Wake locks and their duration
- CPU usage by apps
- Network activity
- Sensor usage (GPS, Bluetooth)
- Any anomalies related to the app com.orienlabs.bridge.wear

Here are the files:
1. Full battery stats: [paste batterystats_full.txt content]
2. App-specific stats: [paste batterystats_bridge.txt content]

Provide a summary of findings and actionable recommendations to reduce battery drain.
```

You can also send these files to developers at **hi@olabs.app** for detailed analysis.