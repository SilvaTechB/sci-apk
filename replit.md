# Sci Archive — Android WebView App

## Overview
A native Android WebView app that loads **https://sci.silvatech.co.ke/**. Built in Java with Gradle (Kotlin DSL).

## Stack
- **Language:** Java
- **Build system:** Gradle 8.4 with Kotlin DSL (`.kts`)
- **Min SDK:** API 21 (Android 5.0 Lollipop)
- **Target SDK:** API 34
- **Package name:** `ke.co.silvatech.sciarchive`

## Features
- Full-screen WebView
- Horizontal progress bar during page loads
- Pull-to-refresh (SwipeRefreshLayout)
- No-internet error screen with Retry button
- Back-button web history navigation
- State preservation on screen rotation
- JavaScript + zoom controls enabled
- Material Design purple theme (no action bar)

## Project Structure
```
SciArchive/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml
│   │   ├── java/ke/co/silvatech/sciarchive/
│   │   │   └── MainActivity.java
│   │   └── res/
│   │       ├── layout/activity_main.xml
│   │       └── values/
│   │           ├── colors.xml
│   │           ├── strings.xml
│   │           └── themes.xml
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── gradle/wrapper/gradle-wrapper.properties
├── build.gradle.kts
├── settings.gradle.kts
└── gradle.properties
```

## How to Build (Android Studio)
1. Open Android Studio → **Open** → select this folder.
2. Let Gradle sync complete.
3. **Build → Clean Project**, then **Build → Rebuild Project**.
4. Connect a device or start an emulator and click **Run ▶**.

> **Note:** The Gradle wrapper binary (`gradle/wrapper/gradle-wrapper.jar`) is not stored in this repo. Android Studio will download it automatically on first sync, or run `gradle wrapper` locally to generate it.

## User Preferences
- Generate all Android source files ready-to-use, no placeholders.
