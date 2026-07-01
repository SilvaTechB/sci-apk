# Sci Archive — Android WebView App

![Platform](https://img.shields.io/badge/Platform-Android-green)
![Min SDK](https://img.shields.io/badge/Min%20SDK-API%2021-blue)
![Language](https://img.shields.io/badge/Language-Java-orange)
![Build](https://img.shields.io/badge/Build-Gradle%20Kotlin%20DSL-purple)

## Overview

**Sci Archive** is a native Android application that loads the website [https://sci.silvatech.co.ke/](https://sci.silvatech.co.ke/) inside a full-screen WebView. It provides a smooth, app-like experience with progress indicators, pull-to-refresh, offline error handling, and full back-navigation support.

---

## Features

| Feature | Description |
|---|---|
| 🌐 Full-screen WebView | Loads the Sci Archive website with no browser chrome |
| 📶 Progress bar | Horizontal bar at the top shows page load progress |
| 🔄 Pull to refresh | Swipe down to reload the current page |
| ⚠️ Offline error screen | Shows a friendly error with a Retry button when there is no internet |
| ⬅️ Back navigation | Back button navigates through browser history before exiting |
| 🔃 Screen rotation | State is preserved when the device is rotated |
| ⚙️ JavaScript enabled | Full JS support for the web app |
| 🔍 Zoom controls | Pinch-to-zoom enabled |
| 🎨 Material Design theme | Purple accent, no action bar, full-screen feel |

---

## Project Structure

```
sci-apk/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── AndroidManifest.xml               # App permissions & activity config
│   │       ├── java/
│   │       │   └── ke/co/silvatech/sciarchive/
│   │       │       └── MainActivity.java          # Core app logic
│   │       └── res/
│   │           ├── drawable/
│   │           │   ├── ic_launcher_foreground.xml # Launcher icon foreground
│   │           │   └── ic_launcher_background.xml # Launcher icon background
│   │           ├── layout/
│   │           │   └── activity_main.xml          # Main screen layout
│   │           ├── mipmap-anydpi-v26/
│   │           │   ├── ic_launcher.xml            # Adaptive icon
│   │           │   └── ic_launcher_round.xml      # Round adaptive icon
│   │           └── values/
│   │               ├── colors.xml                 # Color palette
│   │               ├── strings.xml                # App strings
│   │               └── themes.xml                 # App theme
│   ├── build.gradle.kts                           # Module-level build config
│   └── proguard-rules.pro                         # ProGuard rules
├── gradle/
│   └── wrapper/
│       └── gradle-wrapper.properties              # Gradle version config
├── build.gradle.kts                               # Project-level build config
├── settings.gradle.kts                            # Project settings & repositories
└── gradle.properties                              # JVM & AndroidX flags
```

---

## Tech Stack

| Component | Details |
|---|---|
| Language | Java |
| Build system | Gradle 8.4 with Kotlin DSL (`.kts`) |
| Min SDK | API 21 — Android 5.0 Lollipop |
| Target SDK | API 34 — Android 14 |
| Package name | `ke.co.silvatech.sciarchive` |
| Key library | `androidx.swiperefreshlayout:swiperefreshlayout:1.1.0` |
| UI library | `com.google.android.material:material:1.11.0` |

---

## How It Works

### App Launch
1. Android starts `MainActivity`.
2. The app checks for a network connection via `ConnectivityManager`.
3. If online → the WebView loads `https://sci.silvatech.co.ke/`.
4. If offline → the error screen is shown with a **Retry** button.

### WebView Configuration
- JavaScript is enabled for full web app functionality.
- `shouldOverrideUrlLoading` intercepts all navigation and keeps it inside the app.
- `WebChromeClient.onProgressChanged` drives the top progress bar.
- `onPageFinished` stops the SwipeRefreshLayout spinner when the page is ready.
- `onReceivedError` (both modern API 23+ and legacy) triggers the error screen when a page fails to load.

### Pull to Refresh
- `SwipeRefreshLayout` wraps the WebView.
- On swipe-down, the app re-checks connectivity and calls `webView.reload()`.

### Back Navigation
- `onBackPressed` calls `webView.goBack()` if there is browser history, otherwise exits the app.

### Screen Rotation
- `android:configChanges="orientation|screenSize|keyboardHidden"` in the manifest prevents Activity recreation.
- `onSaveInstanceState` saves the WebView state; `webView.restoreState(savedInstanceState)` restores it in `onCreate`.

---

## Setup & Build Instructions

### Prerequisites
- Android Studio Hedgehog (2023.1.1) or newer
- Android SDK with API 34 installed
- Java 8 or higher

### Steps

#### 1. Open in Android Studio
```
File → Open → select the sci-apk folder
```
Let Gradle sync complete (it downloads dependencies automatically).

#### 2. Build a Debug APK
```
Build → Build Bundle(s) / APK(s) → Build APK(s)
```
Output location:
```
app/build/outputs/apk/debug/app-debug.apk
```

#### 3. Build a Release APK (for distribution)
```
Build → Generate Signed Bundle / APK → APK
```
- Create or select a keystore
- Choose the **release** build variant
- Output: `app/build/outputs/apk/release/app-release.apk`

#### 4. Install on a Device
```bash
# Via ADB
adb install app/build/outputs/apk/debug/app-debug.apk

# Or copy the APK to your phone and open it directly
```

---

## Permissions

| Permission | Reason |
|---|---|
| `INTERNET` | Required to load the website in the WebView |
| `ACCESS_NETWORK_STATE` | Used to detect if the device is online before loading |

---

## Troubleshooting

| Error | Fix |
|---|---|
| `Cannot resolve symbol R` | Build → Clean Project → Rebuild Project |
| `SDK location not found` | SDK Manager → install Android 14 (API 34) |
| `Gradle sync failed` | Check internet; try File → Invalidate Caches → Restart |
| `App not installed` on phone | Enable "Install unknown apps" in phone settings |
| Blank screen on launch | Check internet connection; pull down to trigger refresh |

---

## Developer

**SilvaTech** — [silvatech.co.ke](https://silvatech.co.ke)
