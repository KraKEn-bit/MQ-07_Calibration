# MQ-07_Calibration



# MQ-07 Carbon Monoxide Monitoring System

This project is a collaboration to detect Carbon Monoxide (CO) using an Arduino. 

## 🛠 Hardware Setup
1. **Connect Sensor:** - VCC -> 5V
   - GND -> GND
   - AO  -> A0 (Analog Pin)
2. **Driver Fix:** If your computer doesn't see the Arduino, install the **FT232R USB UART (FTDI)** drivers provided in the repository/links.

---

## 🧪 Step 1: Calibration (For Non-Software Members)
*Every sensor is different. Follow these steps to find your specific "Magic Number" (R0).*

1. Open the folder `Calibration_Tool` and upload `Calibration.ino` to the Arduino.
2. Keep the Arduino plugged into your PC for **15 minutes** (The sensor must get warm to be accurate).
3. Open the **Serial Monitor** (Tools > Serial Monitor).
4. Look for the value labeled `MQ-07 R0 Value`.
5. Once the number stops changing, **write it down**. (Example: 72.5)

---

## 🚀 Step 2: Running the Monitor
1. Open the folder `Final_Monitor` and open `MQ07_Monitor.ino`.
2. Find this line: `const float R0 = 72.5;`
3. Replace `72.5` with the number you wrote down in Step 1.
4. Upload the code.
5. Your Serial Monitor will now show the **exact PPM** of Carbon Monoxide in the air.

---

## 📈 The Formula Used
We use a power-law formula to convert electrical resistance into gas concentration:
**PPM = 100 * (Rs/R0)^-1.53**
