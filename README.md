# Secure GSM-Based Thermal Monitoring and Set-Point Control System
An Embedded C project using LPC2148 and GSM to monitor temperature/humidity, generate SMS alerts, and remotely update set points through password-protected SMS commands.

## 📌 Project Overview

The **Secure GSM-Based Thermal Monitoring and Set-Point Control System** is an embedded system designed for real-time temperature and humidity monitoring with secure remote control using GSM communication.

The system uses an **LPC2148 ARM7 microcontroller** to interface with a DHT11 sensor, LCD, GSM module, EEPROM, keypad, LEDs, and other peripherals. It continuously monitors environmental conditions and compares the measured values with predefined set points.

When the temperature exceeds the configured set point, the system provides a fault indication and sends an **SMS alert with a time stamp** to the authorized mobile number.

## 🚀 Key Features

* Real-time temperature and humidity monitoring using **DHT11**
* **LPC2148 ARM7** based embedded system
* LCD display for sensor readings and system menus
* GSM-based SMS notification and remote control
* Password-protected SMS commands for secure access
* Temperature set-point modification through SMS
* Authorized mobile number modification through SMS
* Remote request for current sensor information
* EEPROM-based storage using **AT24C256**
* Local set-point and password modification using a **4×4 keypad**
* LED/buzzer indication for abnormal conditions
* Password failure indication and temporary blocking after repeated failures
* UART interrupt-based GSM communication
* RTC-based time stamping for alert messages

## 🔧 Hardware Requirements

* LPC2148 ARM7 Microcontroller
* DHT11 Temperature & Humidity Sensor
* GSM Module – M660A
* AT24C256 EEPROM
* LCD
* 4×4 Matrix Keypad
* LEDs / Buzzer
* Switch
* DB-9 Cable / USB-UART Converter

## 💻 Software Requirements

* Keil C Compiler
* Embedded C
* Flash Magic

## 🔄 System Operation

1. The DHT11 sensor continuously measures temperature and relative humidity.
2. The LPC2148 reads the sensor values and displays them on the LCD.
3. The stored set-point values are read from EEPROM.
4. The measured values are compared with the configured set points.
5. If the temperature exceeds its set point, a fault indication is generated and an SMS alert is sent to the authorized user.
6. Incoming SMS messages are checked for the correct password and command syntax.
7. Authorized users can:
   * Change the temperature set point.
   * Change the alert mobile number.
   * Request current sensor information.
8. Local users can also change temperature/humidity set points and the password using the keypad after authentication.

## 📱 SMS Command Format

The system uses the following command structure:
```text
XXXXCDDDD...$
```
Where:
* `XXXX` 	→ 4-digit security password
* `T` 		→ Temperature set-point command
* `M` 		→ Mobile-number command
* `I` 		→ Sensor-information command

### Examples

**Change temperature set point:**

```text
0786T38$
```

**Change authorized mobile number:**

```text
0786M9866666699$
```

**Request current sensor information:**

```text
0786I$
```
The received command is validated before performing any system modification. Invalid commands are discarded.

## 🧩 Main Modules

```text
LPC2148
│
├── DHT11 → Temperature & Humidity
├── LCD → Display
├── GSM M660A → SMS Communication
├── AT24C256 → EEPROM Storage
├── 4×4 Keypad → Local User Input
├── UART → GSM Communication
├── RTC → Time Stamp
└── LEDs/Buzzer → Fault & Security Indication
```
## 📂 Project Structure
```text
Secure-GSM-Thermal-Monitoring/
│
├── main.c
│   └── Main application: sensor monitoring, set-point control,
│       SMS command handling and system control
│
├── gsm.c
├── gsm.h
│   └── GSM M660A driver: initialization, SMS sending and receiving
│       using UART interrupt-based communication
│
├── uart.c
├── uart.h
├── UART_INT.c
│   └── UART polling and interrupt-driven communication
│
├── dht11.c
├── dht11.h
│   └── DHT11 temperature and humidity sensor driver
│
├── i2c.c
├── i2c.h
├── i2c_eeprom.c
├── i2c_eeprom.h
│   └── I²C communication and AT24C256 EEPROM driver for storing
│       set points, password and authorized mobile number
│
├── lcd.c
├── lcd.h
│   └── 16×2 LCD display driver
│
├── keypad.c
├── keypad.h
│   └── 4×4 matrix keypad driver for local user input
│
├── rtc.c
├── rtc.h
│   └── On-chip RTC for time stamping SMS alerts
│
├── eint0.c
│   └── External Interrupt 0 ISR for local configuration access
│
├── menu.c
├── menu.h
│   └── Local set-point and password configuration menu
│
├── delay.c
├── delay.h
│   └── Delay utility functions
│
├── Startup.s
│   └── ARM7 startup and initialization code
│
├── GSM.uvproj
│   └── Keil µVision project file
│
└── major_test.hex
    └── Precompiled firmware for LPC2148
```

### 📁 File Description

| File              | Description                                    |
| ----------------- | ---------------------------------------------- |
| `main.c`          | Main application and system control logic      |
| `gsm.c/.h`        | GSM M660A initialization and SMS communication |
| `uart.c/.h`       | UART communication driver                      |
| `UART_INT.c`      | UART interrupt handling                        |
| `dht11.c/.h`      | Temperature and humidity sensor driver         |
| `i2c.c/.h`        | I²C communication driver                       |
| `i2c_eeprom.c/.h` | AT24C256 EEPROM read/write operations          |
| `lcd.c/.h`        | 16×2 LCD driver                                |
| `keypad.c/.h`     | 4×4 matrix keypad driver                       |
| `rtc.c/.h`        | On-chip RTC and time-stamping                  |
| `eint0.c`         | External Interrupt 0 service routine           |
| `menu.c/.h`       | Local configuration menu                       |
| `delay.c/.h`      | Delay functions                                |
| `Startup.s`       | ARM7 startup code                              |
| `GSM.uvproj`      | Keil µVision project configuration             |
| `major_test.hex`  | Compiled firmware ready for programming        |

> **Note:** The project source files implement the individual peripherals and communication modules described in the project documentation, including LCD, keypad, UART, EEPROM, DHT11 and GSM interfacing.

## 🛠️ Technologies Used

**Microcontroller:** LPC2148 ARM7
**Programming Language:** Embedded C
**Communication:** UART / GSM
**Sensor:** DHT11
**Memory:** AT24C256 EEPROM
**Display:** LCD
**Input:** 4×4 Matrix Keypad
**Development Tool:** Keil C Compiler

## 🎯 Applications

* Industrial temperature monitoring
* Remote environmental monitoring
* Equipment protection
* Industrial automation
* Remote alarm and notification systems
* Temperature-sensitive environments

## 📚 Learning Outcomes

This project provides practical experience in:

* ARM7/LPC2148 microcontroller programming
* Embedded C
* UART and interrupt-based communication
* GSM AT commands
* I²C communication
* EEPROM read/write operations
* Sensor interfacing
* LCD and keypad interfacing
* RTC usage
* Embedded system security and authentication
* Real-time monitoring and alert generation

**Technologies:** Embedded C | LPC2148 ARM7 | GSM | DHT11 | I²C | UART | AT24C256 EEPROM


## 👨‍💻 Author

**Garapati Gowtham Sai Chowdary**

---


