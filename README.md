# **MQ-07 Carbon Monoxide Sensor Calibration & Detection**

## **📌 Overview**
This project explains how to **calibrate and use the MQ-07 gas sensor** with an **Arduino Uno** to detect **Carbon Monoxide (CO)**.

The MQ-07 sensor requires a **special heating cycle** and proper calibration to produce accurate results.  
This repository documents the **complete workflow**, including real problems faced during calibration and how they were solved — written in a beginner-friendly way.

---

## **🧪 What is MQ-07?**
The **MQ-07** is a **Metal Oxide Semiconductor (MOS)** sensor specifically designed to detect **Carbon Monoxide (CO)**.

### **Key Features**
- Detects CO concentration from **10 ppm – 10,000 ppm**
- Sensor resistance **decreases** as CO concentration increases
- Requires a **high-low heating cycle** for accurate readings

---

## **⚙️ How the Sensor Works (Simple Explanation)**
- The sensor has a heating element and a sensitive layer
- When CO gas is present, the layer becomes more conductive
- Higher CO → Lower resistance → Higher voltage output
- Arduino reads this voltage and converts it into **PPM (Parts Per Million)**

---

## **🔌 Pin Description**
The MQ-07 module has **4 pins**:

| Pin | Description |
|----|------------|
| **VCC** | Connects to **5V** |
| **GND** | Connects to **Ground** |
| **DO** | Digital output (HIGH/LOW, threshold-based) |
| **AO** | Analog output (0–5V, used for calibration) |

> ✅ This project uses **Analog Output (AO)** for accurate calibration.

---

## **🧰 Required Components**
- Arduino Uno  
- MQ-07 Gas Sensor Module  
- Jumper Wires  
- USB Cable  
- Arduino IDE  

---

## **⚠️ Important Note (Arduino Driver Issue)**

### **Problem Faced**
Arduino Uno was **not detected** in Arduino IDE due to a missing **FT232R USB-UART driver**.

### **Solution**
Install the **FTDI Virtual COM Port (VCP) driver** manually:

🔗 https://ftdichip.com/drivers/vcp-drivers/

After installation:
- Restart Arduino IDE
- The **COM Port** will appear correctly

---

## **🔥 MQ-07 Heating Cycle**
The MQ-07 sensor operates in a **heating cycle**:

- **High Voltage (5V)** → ~60 seconds (cleans the sensor)
- **Low Voltage** → ~90 seconds (measurement phase)

This cycle improves accuracy and sensor stability.

---

## **🧪 Step-by-Step Calibration Process**

### **Step 1: Sensor Warm-Up**
- Connect **VCC → 5V** and **GND → GND**
- Allow the sensor to warm up for **5–10 minutes**
- This ensures stable and accurate readings

---

### **Step 2: Wiring for Calibration**
- **AO → Arduino A0**
- **GND → Arduino GND**

---

### **Step 3: Upload Calibration Code**
Upload the calibration sketch from this repository:

🔗 **Calibration Code**  
https://github.com/KraKEn-bit/MQ-07_Calibration/blob/main/Calibration_Tool/Callibration_of_Gas_sensor.ino

---

### **Step 4: Monitor Sensor Output**
- Open **Serial Monitor**
- Set **Baud Rate: 9600**
- The sensor prints **R0 values** every few seconds

🕒 **Important:**  
- Initial values fluctuate rapidly  
- Wait **~15 minutes** until the values stabilize

---

### **Step 5: CO Concentration Formula**
To convert sensor readings into PPM, the following **power-law regression formula** is used:

```text
PPM = 100 × (Rs / R0)^(-1.53)
