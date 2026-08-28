# Bridge: User Installation & Platform Guide

## TL;DR

Bridge is a complete code rewrite and is currently in beta testing. Some features may not yet be available or may be buggy. If you encounter an issue, please use the in-app feedback option to contact the developer. An in-app data migration option is available on a best-effort basis; migration may be incomplete or unavailable for some legacy data.

**Install quickly:**

* **iPhone:** Install [Bridge through TestFlight](https://testflight.apple.com/join/cNQxMjAu).
* **Wear OS watch:** Download the latest watch APK from the [GitHub Releases page](https://github.com/orienlabs/bridge_app/releases), then install it using ADB or transfer it to the watch with the [File Browser app](https://play.google.com/store/apps/details?id=com.orienlabs.filebrowser.wear) and open the APK there.
* **Apple Watch:** Install the watch app through TestFlight after installing Bridge on your iPhone.

> [!IMPORTANT]
> **Important Notice: Bridge Rebuilt from Scratch**
> 
> We are completely rebuilding the Bridge application from the ground up to deliver a true, cross-platform experience across both Apple and Android ecosystems. As part of this major transition, please note:
> 
> * **Broader Device Support:** We have lowered the minimum required operating system versions so that Bridge can support older phone and watch models.
> * **Best-Effort Data Migration:** An in-app migration option is available for data from previous legacy apps, but migration may be incomplete or unavailable for some data.
> * **Coordinated Upgrades Required:** Due to a new custom communication protocol, **both your phone and watch apps must be upgraded to the new version to pair and sync**. New versions of the app cannot pair with older legacy versions.

## 1. What is Bridge & Why Does It Exist?

Smartwatches and smartphones are traditionally locked to their respective ecosystems, leaving users with limited choices if they want to mix and match devices. For instance, pairing an Apple Watch with an Android phone is natively unsupported, and using a Wear OS smartwatch with an iPhone often severely limits its functionality. 

Bridge breaks down these platform barriers. By utilizing a custom, power-efficient Bluetooth communication protocol, Bridge allows any supported smartwatch to pair and sync directly with any supported smartphone. Whether you need notification mirroring, health and activity data syncing, or media playback controls, Bridge acts as a universal link to keep your devices connected—regardless of brand or operating system.

### Compatibility Matrix
Below is a table showing the supported smartwatch and smartphone combinations, along with the features available for each pair:

> [!TIP]
> **Multi-Device Pairing Support:** Bridge now supports multi-device pairing on both sides. A single smartwatch can be paired with multiple smartphones (e.g., both your personal and work phones), and a single smartphone can connect to and manage multiple smartwatches simultaneously.

| Smartwatch Platform | Smartphone Platform | Key Features Supported |
| :--- | :--- | :--- |
| **Apple Watch** (watchOS) | **iPhone** (iOS) | Notification mirroring, Health/Workout data sync, Media controls, Settings synchronization |
| **Apple Watch** (watchOS) | **Android Phone** | Notification mirroring, Workout data sync, Media playback controls |
| **Wear OS Watch** | **iPhone** (iOS) | Notification mirroring, Health sync (integrates with Apple Health), Media controls |
| **Wear OS Watch** | **Android Phone** | Notification mirroring, Health sync (integrates with Google Health Connect), Media controls |

### Supported OS Versions & Platform Limits
Below are the minimum software requirements and specific platform considerations verified directly from the application's configuration:

| Device Platform | Minimum OS Version Supported | Key Capabilities & Limitations |
| :--- | :--- | :--- |
| **Android Phone** | Android 8.0 (Oreo / API 26) or later | • Notification mirroring and media controls require Android 8.0+.<br>• **Health Data Sync (Health Connect)** requires Android 9.0+ (downloadable from Google Play) or Android 14+ (built directly into the system). |
| **Android Wear OS Watch** | Wear OS 2.0 (Android 8.0 / API 26) or later | • Basic notification mirroring and media control require Wear OS 2.0+.<br>• **Health Data Sync** is **only available on Wear OS 3.0 (Android 11 / API 30) or higher** due to system requirements for Google Health Services. |
| **iPhone (iOS)** | iOS 15.0 or later | • Full notification and health sync features require iOS 15.0+.<br>• Background syncing requires Bluetooth Sharing and Background App Refresh enabled. iOS may restrict background activity if the app remains closed for long periods. |
| **Apple Watch (watchOS)** | watchOS 9.6 or later | • Supports native workout tracking and heart rate sync.<br>• Continuous health recording in the background requires Workout Session permissions.<br>• Beta testing via TestFlight is not supported on Family Setup watches. |

---

## 2. Requesting Early Access (Beta Testing)

Bridge is currently in **private internal testing**. To download and install the applications, your account IDs must first be added to our authorized tester lists.

### Step 1: Submit Your Tester IDs
Click here to [Request Early Access](mailto:bridge@olabs.app?subject=Request%20for%20Bridge%20Early%20Access&body=Hello,%0A%0AI%20would%20like%20to%20request%20early%20access%20to%20the%20Bridge%20beta.%20Here%20are%20my%20details:%0A%0A-%20Apple%20ID%20(for%20TestFlight/iOS):%20%0A-%20Google%20Play%20Email%20(for%20Android/Wear%20OS):%20%0A%0AThanks!). This will open a draft email in your default mail client with `bridge@olabs.app` pre-filled.

Fill in your:
* **Apple ID** (to receive the TestFlight invitation for iPhone and Apple Watch).
* **Google Play Email** (to be added to the Google Play Console internal test track for Android and Wear OS).

Once we add your accounts, we will reply with your official download links for TestFlight and Google Play.

### Step 2: Alternative APK Installation (Android Only)
If you prefer not to wait for Google Play Console provisioning, Android and Wear OS users can download the raw app packages (APKs) directly from our [GitHub Release Page](https://github.com/orienlabs/bridge_app/releases/) and install them manually.

---

## 3. Installation Guide for Apple Devices (iPhone & Apple Watch)

Once your Apple ID has been added to our tester list, install TestFlight and open the [Bridge TestFlight invitation link](https://testflight.apple.com/join/cNQxMjAu) on your iPhone:

### A. Installing on your iPhone
1. Install the **TestFlight** app from the App Store if you don't have it.
2. Open the [Bridge TestFlight invitation link](https://testflight.apple.com/join/cNQxMjAu).
3. Tap **View in TestFlight** if prompted.
4. Accept the invitation for **Bridge** in the TestFlight app and tap **Install**.

### B. Installing on a Standard Apple Watch (Paired to your iPhone)
If your Apple Watch is paired to your personal iPhone:
1. Open the **TestFlight app on your iPhone**.
2. Tap on the **Bridge** app in your test list.
3. Scroll down to the **Apple Watch** section and tap **Install** to deploy it to your watch.

### C. Installing on a Family Setup Apple Watch (No Paired iPhone)
If you are setting up the watch for a family member (like a child or senior) who does not have their own iPhone:
1. *Note: Since TestFlight is not supported on Family Setup watches, the app must be installed via the App Store once released, or directly sideloaded via Xcode during development testing.*
2. Once the app is publicly released (or distributed via Unlisted link), the user can open the **App Store app directly on the Apple Watch**, search for **Bridge**, and download it directly.

---

## 4. Installation Guide for Android Devices (Android Phone & Wear OS)

Once your Google Play Email has been added to our tester list and you receive your testing link:

### A. Installing on your Android Phone
1. Open the testing invitation link sent to your Google Play email.
2. Tap **Join on Web** or **Join on Android** to opt into the internal testing program.
3. Use the link provided to download **Bridge** from the Google Play Store.
4. *(Alternative)* Download the phone APK directly from the [GitHub Release Page](https://github.com/orienlabs/bridge_app/releases/) and open it on your phone to install (requires enabling "Install unknown apps" permission).

### B. Installing on your Wear OS Smartwatch
1. **Direct APK Installation via ADB:**
   * Download the Wear OS APK from the [latest GitHub Release](https://github.com/orienlabs/bridge_app/releases).
   * Transfer the APK to the watch and install it using ADB. See the [ADB installation guide](guides/install-via-adb.md).
2. **Alternative File-Browser Installation:**
   * Transfer the APK to the watch with the [File Browser app](https://play.google.com/store/apps/details?id=com.orienlabs.filebrowser.wear).
   * Open the APK on the watch and follow the installation prompts, if the file-browser app supports APK installation.

---

## 5. Keeping Your Apps Up to Date

For the best experience, we recommend keeping automatic updates turned on:
* **Apple Watch:** Go to Settings ➜ App Store on your watch and turn on **Automatic Downloads**.
* **Wear OS Watch:** Open the Play Store on your watch, swipe down to Settings, and turn on **Auto-update apps**.
* **Phones:** Enable auto-updates in the App Store (iOS) or Google Play Store (Android).

---

## 6. Need Help?

If you run into any issues during the installation, pairing, or data synchronization process:
* Verify that both devices have Bluetooth and Wi-Fi enabled.
* Make sure you have authorized all requested permissions (such as Bluetooth, Background Sync, and Health Access) during onboarding.
* Contact the developer team directly by emailing us at [bridge@olabs.app](mailto:bridge@olabs.app).
