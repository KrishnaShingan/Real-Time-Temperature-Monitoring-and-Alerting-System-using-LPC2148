🌡️ Real-Time Temperature Monitoring and Alerting System

Using LPC2148, GSM & RTC

📌 Project Overview

This project implements a Real-Time Temperature Monitoring and Alerting System using the LPC2148 ARM7 microcontroller.
The system continuously monitors temperature using an ADC-based sensor, displays values on an LCD, and provides remote monitoring and configuration through GSM (SMS).

The system also integrates a Real-Time Clock (RTC) to timestamp alerts, making the system suitable for industrial and safety-critical applications.

🎯 Key Features

Real-time temperature monitoring

GSM-based SMS alert system

Secure SMS command processing using passkey

EEPROM-based storage for mobile number & set point

RTC-based date & time stamping of alerts

Interrupt & timer-driven architecture

LCD, keypad, buzzer & LED indications

🧱 Project File Structure

├── Main.c        → Main control loop & alert logic

├── GSM.c         → GSM init, SMS send/receive, command processing

├── UART.c        → UART0 driver for GSM

├── EEPROM.c      → Non-volatile storage (mobile number, set point, passkey)

├── RTC.c         → Real Time Clock functions (date & time)

├── Timer0.c      → Periodic temperature sampling

├── Interrupt.c   → UART & timer interrupts

├── Keypad.c      → Local user input

├── LCD.c         → 16x2 LCD interface

├── ADC.c         → Temperature sensor reading

└── *.h           → Header files


🔁 System Working Flow

System Initialization

LCD, UART0, GSM, ADC, RTC, EEPROM, Timer0 initialized

Stored mobile number, set point, and passkey loaded from EEPROM

Temperature Monitoring

ADC reads sensor value

Converted to temperature (°C)

Displayed on LCD continuously

Timer-Based Execution

Timer0 interrupt triggers periodic updates

Ensures non-blocking real-time operation

Threshold Comparison

Current temperature compared with stored set point

Alert Generation

If temperature exceeds set point:

Buzzer ON

SMS alert sent with date & time from RTC

Alert sent only once per event

SMS Command Processing

Incoming SMS validated

Passkey checked

Command executed

Response SMS sent

⏰ RTC (Real Time Clock) Usage

The RTC is used to timestamp alert messages.

Example Alert SMS:
Alert: The current temperature(45) has exceeded the configured set point (38)
@ 18-09-2025 14:32:10


RTC functions are implemented in RTC.c.

📩 SMS Message Structure (IMPORTANT)

All SMS commands must follow this secure format:

<4-digit PASSKEY><COMMAND><DATA>$

🔐 Passkey

First 4 digits

Stored in EEPROM

Example: 0786

🔚 End Marker

$ must be the last character

Ensures message integrity

📜 Supported SMS Commands

1️⃣ Update Temperature Set Point
0786T38$


Meaning:

0786 → Passkey

T → Set temperature command

38 → New set point

$ → End marker

✔ Stored in EEPROM
✔ Confirmation SMS sent

2️⃣ Update Mobile Number
0786M9866666699$


✔ Updates alert mobile number
✔ Stored in EEPROM
✔ Normalizes country code automatically

3️⃣ Get Current Temperature
0786I$


Response:

The current temperature is 32 degree Celsius.

4️⃣ Get Current Set Point
0786S$


Response:

The current set point is 38 degree Celsius.
Thank you.

🚨 Alert SMS Format (With RTC)
Alert: The current temperature(45) has exceeded the configured set point (38)
@ DD-MM-YYYY HH:MM:SS


✔ Sent only once per threshold breach
✔ Prevents SMS flooding

💡 LED & Buzzer Indications
Indicator	Status	Meaning
Power LED	ON	System running
GSM LED	Blinking	GSM communication
Alert LED	ON	Temperature exceeded
Buzzer	ON	Alert condition
Alert Flag	Set	SMS sent successfully
🖥️ LCD Display Format
TEMP: 32 C
SET : 38 C

💾 EEPROM Usage
Data	Purpose
Mobile Number	Alert destination
Set Point	Temperature threshold
Passkey	SMS authentication

✔ Data retained after power failure

🔧 Hardware Components

LPC2148 ARM7 Microcontroller

LM35 Temperature Sensor

GSM Module (SIM800 / SIM900)

RTC (Internal LPC2148 RTC)

16x2 LCD

Keypad

Buzzer

LEDs

Regulated Power Supply

🧪 Applications

Industrial temperature monitoring

Server room safety systems

Remote sensor monitoring

Embedded security systems

Academic ARM7 projects

👨‍💻 Author

Krishna Shingan
Embedded Systems | ARM7 | GSM | RTC

📜 License

This project is intended for academic and educational use only.
