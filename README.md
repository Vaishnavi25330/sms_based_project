
**Project Title: SMS-Based Thermal Monitoring and Threshold Management**

**Overview:**

This project is a real-time embedded system for monitoring and managing temperature using an LM35 sensor and controlling alerts via SMS. It is ideal for environments where temperature needs to be strictly maintained, such as:

* Industrial sites
* Server rooms
* Cold storage

The system uses a GSM module to communicate via SMS, and users can configure threshold values and receive alerts from anywhere.

---
**Block Diagram:**

![image](https://github.com/user-attachments/assets/408224df-b09d-43e7-a73c-774c6e100025)


**Features:**

* SMS-based remote control and configuration
* Real-time temperature monitoring displayed on 16x2 LCD
* Threshold breach detection with buzzer alert
* SMS alert to a stored mobile number
* Passkey protection for security
* EEPROM storage for threshold and authorized number
* Optional RTC for timestamping

---

**Hardware Requirements:**

* LPC2148 Microcontroller
* GSM Module (M660A)
* LM35 Temperature Sensor
* 16x2 LCD Display
* AT25LC512 EEPROM
* Buzzer
* RTC (optional)

---

**Software Requirements:**

* Embedded C programming
* Keil uVision IDE
* Flash Magic tool for burning hex files

---

**Folder Structure (Project Files):**

* lcd.c, lcd.h
* uart.c, uart.h
* spi.c, spi.h
* adc.c, adc.h
* eeprom.c, eeprom.h
* gsm.c, gsm.h
* buzzer.c, buzzer.h
* delay.c, delay.h
* defines.h
* projectmain.c

---

**Testing Steps:**

1. Test LCD for displaying characters and strings.
2. Test keypad (if used) for key detection.
3. Test EEPROM read/write using BYTE WRITE and BYTE READ functions.
4. Test UART communication using interrupts.
5. Test RTC (if used) by reading time and displaying on LCD.
6. Test GSM module via PC using AT commands:

   * AT
   * ATE0
   * AT+CMGF=1
   * AT+CNMI=2,1,0,0,0
   * AT+CMGD=1
   * AT+CMGR=1
   * AT+CMGS="Mobile Number" (followed by message and Ctrl+Z)

---

**Main Program Flow:**

1. Initialize peripherals.
2. Continuously read temperature from LM35.
3. Display current temperature on LCD.
4. Read stored threshold from EEPROM.
5. If current temp > threshold:

   * Sound buzzer
   * Send alert SMS
6. If SMS is received:

   * Check message format and passkey
   * Parse command:

     * 'T' = Update temperature threshold
     * 'M' = Update mobile number
     * 'I' = Request sensor status
   * Act accordingly and send SMS reply

---

**SMS Message Format:**

```
XXXXCMD...$
Where:
XXXX = 4-digit passkey  
C = Command Type [T for temperature, M for mobile number, I for info]  
D... = Data
```

**Examples:**

* Set threshold to 38°C → `0786T38$`
* Change mobile number → `0786M9876543210$`
* Request sensor info → `0786I$`

*Only messages from the authorized number saved in EEPROM will be accepted.*

---

**Completion Checklist:**

* Temperature display and alerts work correctly
* SMS alerts sent when threshold is crossed
* SMS commands accepted and processed securely
* EEPROM stores and retrieves configuration properly

---

**End Note:**

This project showcases embedded systems, sensor integration, serial communication, EEPROM handling, and GSM-based control in real-world scenarios.

