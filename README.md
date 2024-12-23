# Buildozer and APK Conversion Guide

This guide provides a detailed walkthrough for setting up Buildozer and converting your Python app into an APK. It includes solutions to common errors and troubleshooting steps to ensure a smooth process.

---

## Table of Contents
1. [Installation and Setup](#installation-and-setup)
2. [Preparing Your Project](#preparing-your-project)
3. [Configuring Buildozer](#configuring-buildozer)
4. [Building the APK](#building-the-apk)
5. [Common Errors and Fixes](#common-errors-and-fixes)
6. [Troubleshooting Gradle Issues](#troubleshooting-gradle-issues)

---

## Installation and Setup

### Prerequisites
Ensure your system meets the following requirements:
- **OS:** Linux or WSL2 on Windows
- **Python:** 3.9+ (Python 3.11 preferred)
- **Dependencies:**
  ```bash
  sudo apt update && sudo apt install -y \
      git zip unzip openjdk-11-jdk python3-pip libffi-dev \
      libssl-dev build-essential libzbar-dev
  ```

### Install Buildozer
1. Create and activate a virtual environment:
   ```bash
   python3 -m venv buildozer-env
   source buildozer-env/bin/activate
   ```

2. Install Buildozer and Cython:
   ```bash
   pip install buildozer Cython
   ```

3. Install the Android SDK and NDK:
   ```bash
   buildozer android update
   ```

---

## Preparing Your Project

Ensure your project has the following structure:
```
project-directory/
├── main.py  # Your app's entry point
├── buildozer.spec  # Auto-generated configuration file
├── assets/  # Optional assets directory
└── requirements.txt  # Python dependencies (if any)
```

### Generate the `buildozer.spec` file:

Navigate to your project folder
```bash
cd /mnt/c/Users/YOUR_USERNAME/OneDrive/Desktop/YOURGAMEFOLDER
```
Generate the `buildozer.spec` file:
```bash
buildozer init
```

---

## Configuring Buildozer

Edit the `buildozer.spec` file to set your app's properties. Key fields to configure:
- `title`: Name of your app.
- `package.name`: Package name (e.g., `org.example.myapp`).
- `requirements`: List of Python dependencies (e.g., `kivy, requests`).
- `android.api`: Target Android API (default: 31).
- `android.arch`: Supported architectures (e.g., `arm64-v8a`).

---

## Building the APK

### Step 1: Navigate to your project folder
```bash
cd /mnt/c/Users/YOUR_USERNAME/OneDrive/Desktop/YOURGAMEFOLDER
```
 
### Step 2: Run Buildozer
To create an APK in debug mode:
```bash
buildozer -v android debug
```

### Step 3: Find the Output APK
Once the build succeeds, find the APK in:
```
/path/to/your/project/bin/yourgame.apk
```

### Step 4: Test the APK
Transfer the APK to your Android device and install it to test.

---

---

## Common Errors and Fixes

### 1. `ModuleNotFoundError` for `distutils`
**Error:**
```bash
ModuleNotFoundError: No module named 'distutils'
```
**Solution:**
Install the required package:
```bash
sudo apt install python3-distutils
```

### 2. Missing `ctypes`
**Error:**
```bash
ModuleNotFoundError: No module named '_ctypes'
```
**Solution:**
Install development libraries:
```bash
sudo apt install libffi-dev
```

### 3. Missing `zip` Command
**Error:**
```bash
sh.CommandNotFound: zip
```
**Solution:**
Install `zip`:
```bash
sudo apt install zip
```

### 4. Unsupported Gradle Version
**Error:**
```bash
Unsupported class file major version 65
```
**Solution:**
Update your Gradle version by modifying the `gradle-wrapper.properties` file or reinstalling the Android SDK:
```bash
buildozer android update
```

---

## Troubleshooting Gradle Issues

### 1. Incompatible Gradle Versions
Ensure your Gradle version matches your Android SDK and Java installation.
- Open the `gradle-wrapper.properties` file located in the `build/` directory.
- Update the Gradle distribution URL to the desired version:
  ```properties
  distributionUrl=https\://services.gradle.org/distributions/gradle-7.6-all.zip
  ```

### 2. Clearing Gradle Cache
If you encounter cache-related issues, clear the Gradle cache:
```bash
rm -rf ~/.gradle/caches
```

### 3. Updating the Android SDK
Reinstall or update the Android SDK:
```bash
buildozer android update
```

### 4. Debugging Gradle Builds
Run Buildozer with additional debug output to pinpoint Gradle issues:
```bash
buildozer -v android debug --info
```

---

This guide will help you successfully set up Buildozer, resolve common errors, and convert your Python app into an APK. For further assistance, refer to the [Buildozer documentation](https://buildozer.readthedocs.io/) or [python-for-android documentation](https://python-for-android.readthedocs.io/).
