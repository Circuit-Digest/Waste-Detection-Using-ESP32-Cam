# 🗑️ Waste Detection Using ESP32-CAM with CircuitDigest Cloud API

<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32--CAM-blue?style=for-the-badge&logo=espressif" />
  <img src="https://img.shields.io/badge/AI-CircuitDigest%20Cloud-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Language-C%2B%2B%20(Arduino)-orange?style=for-the-badge&logo=arduino" />
  <img src="https://img.shields.io/badge/Protocol-HTTPS-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" />
</p>

<p align="center">
  An AI-powered waste detection system that uses an <strong>ESP32-CAM</strong> to capture images and classifies them as <strong>Biodegradable</strong> or <strong>Non-Biodegradable</strong> using the <strong>CircuitDigest Cloud API</strong> — no ML training required!
</p>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [How It Works](#-how-it-works)
- [Components Required](#-components-required)
- [Circuit Diagram](#-circuit-diagram)
- [Getting Started](#-getting-started)
  - [Step 1: Create a CircuitDigest Cloud Account](#step-1-create-a-circuitdigest-cloud-account)
  - [Step 2: Get Your API Key](#step-2-get-your-api-key)
  - [Step 3: Test the API Virtually](#step-3-test-the-api-virtually)
  - [Step 4: Hardware Setup & Code Upload](#step-4-hardware-setup--code-upload)
- [Code Explanation](#-code-explanation)
- [Output](#-output)
- [Advantages & Limitations](#-advantages--limitations)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Relevant Links](#-relevant-links)
- [License](#-license)

---

## 🌍 Overview

In our daily lives, huge amounts of waste are generated in homes, streets, offices, and public places. The real problem is not just collecting the waste — it is **separating it correctly**. When biodegradable waste (food scraps, leaves) gets mixed with non-biodegradable waste (plastic bottles, metal cans), recycling becomes difficult and environmental pollution increases.

This project solves that problem with a compact, low-cost, AI-powered system:

> **Press a button → Camera captures waste image → Cloud AI classifies it → Result shown in Serial Monitor also the LED indication for different wastes**

No expensive hardware. No complex ML training. Just plug, configure, and detect! ⚡

---

## ⚙️ How It Works

```
[ Push Button Pressed ]
        ↓
[ ESP32-CAM Captures Image ]
        ↓
[ Image Sent via Wi-Fi over HTTPS ]
        ↓
[ CircuitDigest Cloud API Processes Image with AI ]
        ↓
[ Result Returned: Biodegradable / Non-Biodegradable / Life ]
        ↓
[ Output Displayed on Serial Monitor ]
```

---

## 🧰 Components Required

| S.No | Component | Purpose |
|------|-----------|---------|
| 1 | ESP32-CAM | Microcontroller with built-in camera & Wi-Fi |
| 2 | Push Button | Triggers image capture on press |
| 3 | Breadboard | Simplifies and organizes circuit connections |
| 4 | USB-to-Serial (FTDI) Adapter *(if needed)* | For programming standard ESP32-CAM without onboard USB |
| 5 | USB Cable | Powers the entire system via laptop/PC |
| 6 | Red and Green LED | Used as the indications for the different wastes.

> **⚠️ Note:** If you are using the standard ESP32-CAM (without onboard USB), you need a **USB-to-Serial (FTDI) adapter** for programming.
> - FTDI TX → ESP32-CAM RX (U0R)
> - FTDI RX → ESP32-CAM TX (U0T)
> - GND → GND
> - Hold **GPIO0 LOW** during upload to enter flash mode.

---

## 🚀 Getting Started

### Step 1: Create a CircuitDigest Cloud Account

Go to the [CircuitDigest Cloud website](https://circuitdigest.cloud), create a free account, and log in.

### Step 2: Get Your API Key

- Navigate to the **Waste Detection** section from the dashboard.
- Your **API Key** will be displayed on the left panel under your account settings.
- Note the **confidence level** setting — adjust it based on your needs.

> 📊 **API Limits:** 15 requests/day and 100 requests/month on the free tier.

### Step 3: Test the API Virtually

- Use the **"Try API"** feature on the dashboard.
- Upload a sample image of biodegradable or non-biodegradable waste.
- Click **"Run Test"** — results will be displayed within seconds.
- Test with multiple images to evaluate accuracy before moving to hardware.

### Step 4: Hardware Setup & Code Upload

1. Connect all components as per the circuit diagram.
2. Open the Arduino IDE and install the **ESP32 board package**.
3. Open the project code and update the following credentials:
4. Select **AI Thinker ESP32-CAM** as the board.
5. Upload the code. Hold **GPIO0 LOW** if using FTDI.
6. Open the **Serial Monitor** at **115200 baud**.
7. Press the push button — the result will appear within seconds!

---

## 📊 Output

After pressing the push button:

```
Connecting to WiFi...
WiFi Connected!
Button Pressed - Capturing Image...
Image Captured. Sending to API...
API Response: Non-Biodegradable
Red Led will glow
```

Results can be:
- ✅ **Biodegradable** — Food waste, leaves, paper, etc.
- 🚫 **Non-Biodegradable** — Plastic, metal, glass, etc.
- 🌿 **Life** — Living organisms detected in the image

---

## ✅ Advantages & Limitations

| S.No | Advantages | Limitations |
|------|------------|-------------|
| 1 | Real-time waste detection within seconds | Cannot work without cloud API access |
| 2 | Low-cost system using ESP32-CAM with built-in camera & Wi-Fi | Requires an active internet connection |
| 3 | No expensive hardware or powerful processors needed | Blurry images may give incorrect results |
| 4 | Fully wireless communication | Limited by daily/monthly API usage limits |
| 5 | Small size and portable design | Captures single images, not live video detection |

---

## 🛠️ Troubleshooting

### ❌ Issue 1: Camera Capture Failed (Memory Allocation)
- **Cause:** Insufficient PSRAM for high-resolution images.
- **Fix:** Reduce frame size, lower JPEG quality, or enable PSRAM in board settings.

### 🔄 Issue 2: ESP32-CAM Restarting Automatically
- **Cause:** Unstable USB power from laptop port.
- **Fix:** Use an **external power supply**. Double-check all wiring connections.

### 🌫️ Issue 3: Blurry or Low-Quality Images
- **Cause:** Incorrect lens focus or poor lighting.
- **Fix:** Manually rotate the camera lens to focus. Ensure adequate lighting and adjust brightness/contrast parameters.

### 🚫 Issue 4: Camera Initialization Failed
- **Cause:** Wrong board selection, incorrect GPIO mapping, or insufficient power.
- **Fix:** Select **AI Thinker ESP32-CAM** in Arduino IDE. Verify GPIO pin configuration matches your board.

### 🤔 Issue 5: No Detection or Incorrect Results
- **Cause:** Poor image quality, bad lighting, or low confidence threshold.
- **Fix:** Ensure proper lighting, steady camera angle, and adjust the **confidence threshold** in the API dashboard.

---

## ❓ FAQ

**1. Why is the cloud API used instead of local processing?**
> The ESP32-CAM has limited memory and processing power. Cloud API performs heavy AI inference on powerful servers, giving better accuracy and faster results.

**2. What happens when the push button is pressed?**
> The ESP32-CAM captures a JPEG image and sends it to the CircuitDigest Cloud API via HTTPS. The API classifies the waste and returns the result, which is displayed on the Serial Monitor.

**3. Can this system detect multiple waste types at the same time?**
> Yes! If multiple waste objects are visible in a single image, the API can identify different categories depending on the model's supported classes.

**4. Can this system work without an internet connection?**
> No. The system requires an active internet connection because all detection and classification happen on the cloud server.

**5. How can detection accuracy be improved?**
> Ensure proper lighting, clear focus, correct camera angle, and fine-tune the **confidence threshold** in the API settings dashboard.

---

## 🔗 Relevant Links

- 📦 **GitHub Repository:** [Circuit-Digest/Waste-Detection-Using-ESP32-Cam](https://github.com/Circuit-Digest/Waste-Detection-Using-ESP32-Cam)
- ☁️ **CircuitDigest Cloud:** [circuitdigest.cloud](https://circuitdigest.cloud)
- 📧 [Send Email using ESP32 with CircuitDigest Cloud](https://circuitdigest.com/microcontroller-projects/how-to-send-email-using-esp32-circuitdigest-cloud)
- 📧 [Send Email using Arduino with CircuitDigest Cloud](https://circuitdigest.com/microcontroller-projects/how-to-send-email-notification-using-arduino-circuitdigest-cloud)
- 📧 [Send Email using Raspberry Pi Pico with CircuitDigest Cloud](https://circuitdigest.com/microcontroller-projects/send-email-notification-using-raspberry-pi-pico-circuitdigest-cloud)

---

<p align="center">
  Made with ❤️ by <a href="https://circuitdigest.com">CircuitDigest</a> | Powered by <a href="https://circuitdigest.cloud">CircuitDigest Cloud AI</a>
</p>
