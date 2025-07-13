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

code:
#include <Wire.h>
#include "RTClib.h"

RTC_DS1307 rtc;

// Segment pins A to G
const int segmentPins[7] = {2, 3, 4, 5, 6, 7, 8};

// Digit cathode control pins
const int digitPins[4] = {9, 10, 11, 12};

// Segment codes for 0-9
const byte digitCode[10] = {
  B00111111, // 0
  B00000110, // 1
  B01011011, // 2
  B01001111, // 3
  B01100110, // 4
  B01101101, // 5
  B01111101, // 6
  B00000111, // 7
  B01111111, // 8
  B01101111  // 9
};

void setup() {
  Wire.begin();
  rtc.begin();
  // rtc.adjust(DateTime(F(_DATE), F(TIME_))); // Uncomment once to set time

  for (int i = 0; i < 7; i++) pinMode(segmentPins[i], OUTPUT);
  for (int i = 0; i < 4; i++) pinMode(digitPins[i], OUTPUT);
}

void loop() {
  DateTime now = rtc.now();

  int hour = now.hour();
  int minute = now.minute();

  int digits[4] = {
    hour / 10,
    hour % 10,
    minute / 10,
    minute % 10
  };

  for (int i = 0; i < 4; i++) {
    showDigit(i, digits[i]);
    delay(5);
    clearDigits();
  }
}

void showDigit(int digitIndex, int number) {
  byte segments = digitCode[number];
  for (int s = 0; s < 7; s++) {
    digitalWrite(segmentPins[s], bitRead(segments, s));
  }
  digitalWrite(digitPins[digitIndex], LOW); // Enable digit
}

void clearDigits() {
  for (int i = 0; i < 4; i++) {
    digitalWrite(digitPins[i], HIGH); // Disable all
  }
}


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
