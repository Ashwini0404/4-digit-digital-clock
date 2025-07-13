# 4-Digit Digital Clock using Arduino

## 🔧 Components Used
- Arduino Uno board  
- DS1307 Real-Time Clock (RTC) module  
- 4-digit 7-segment display (common cathode)  
- 4 × 200Ω resistors  
- 32.768 kHz crystal oscillator  
- 2 × 22pF ceramic capacitors  
- Jumper wires 
- Proteus software for simulation  

## 📘 Project Overview
This project displays real-time hours and minutes in HHMM format using a 4-digit 7-segment display. It works with an Arduino Uno and a DS1307 RTC module. Even during power cuts, the time continues accurately due to the backup battery in the RTC.

The display is driven using multiplexing, which reduces the number of Arduino pins needed.

## 🧠 How It Works
- DS1307 communicates time to Arduino using I2C (SDA/SCL).
- Arduino reads the time, extracts hours and minutes.
- A multiplexing technique is used to activate each digit quickly one after the other.
- Proteus was used to simulate and verify the design.

## 📁 Files in This Repository
| File Name | Description |
|-----------|-------------|
| `4 digit 7 seg code.pdf` | Contains Arduino source code |
| `4 digit 7 segment display clock.pdsprj` | Proteus simulation file |
| `Screenshot 2025-07-13 145325.png` | Image of simulation output |
| `README.md` | Project explanation |

## ✅ Highlights
- Real-time display using RTC
- Multiplexed 4-digit 7-segment output
- Works even after reset (because of RTC battery)
- Code and simulation verified

## 👩‍💻 Developed By
**Kogilamane Ashwini**  
GitHub: [Ashwini0404](https://github.com/Ashwini0404)

---

## 💡 Future Enhancements
- Include alarm functionality  
- Interface LM35 to show temperature  
