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

🔌 LPC2148 Pin Configuration

📍 PORT 0 Assignments

Pin	Function	Description

P0.0	UART0 TX	Transmit data to GSM module (RX of GSM)

P0.1	UART0 RX	Receive data from GSM module (TX of GSM)

P0.2	I2C SCL	Serial Clock line for EEPROM

P0.3	I2C SDA	Serial Data line for EEPROM

P0.5	LCD RS	Register Select for LCD

P0.6	LCD EN	Enable signal for LCD

P0.16	EINT0	External interrupt switch

P0.20	LED	Blink control indicator

P0.21	LED	EEPROM error indication

P0.22	LED	GSM error indication

P0.25	Buzzer	Alert buzzer output

P0.28	ADC	Temperature sensor (LM35) input

📍 PORT 1 Assignments

Pin	Function	Description

P1.16	LCD D0	LCD data bit 0

P1.17	LCD D1	LCD data bit 1

P1.18	LCD D2	LCD data bit 2

P1.19	LCD D3	LCD data bit 3

P1.20	LCD D4	LCD data bit 4

P1.21	LCD D5	LCD data bit 5

P1.22	LCD D6	LCD data bit 6

P1.23	LCD D7	LCD data bit 7

P1.24	Keypad	Keypad row/column

P1.25	Keypad	Keypad row/column

P1.26	Keypad	Keypad row/column

P1.27	Keypad	Keypad row/column

P1.28	Keypad	Keypad row/column

P1.29	Keypad	Keypad row/column

P1.30	Keypad	Keypad row/column

P1.31	Keypad	Keypad row/column

📝 Notes

UART0 is dedicated to GSM communication

I2C interface is used for EEPROM storage

LCD operates in 8-bit mode

ADC input reads temperature from LM35

RTC works internally using LPC2148 RTC registers

LEDs provide system & error status

Buzzer activates during temperature alert

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

📜 License

This project is intended for academic and educational use only.


