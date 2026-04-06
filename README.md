# Task 1: Push Button Counter System
​### 1. Project Objective
​The goal is to create an embedded system using an Arduino Uno (ATmega328P) that detects a physical button press and increments a numerical counter. The count is then displayed in real-time via the Serial Monitor. A critical part of this task is implementing software debouncing to ensure accuracy.
​### 2. Hardware Components & Connections
​Microcontroller: Arduino Uno.
​Input Device: Momentary Push Button.
​Connection Port: Digital Pin 2 (PD2 in AVR terms).
​Resistor Logic: A 10k \Omega resistor is used to ensure the pin has a defined state (High or Low) when the button is not pressed.
​### 3. Technical Implementation (Software Logic)
​Your project uses Direct Port Manipulation in Embedded C, which is much faster than standard Arduino functions.
​Baud Rate: Set to 9600 for UART (Serial) communication.
​Polling Method: The CPU constantly checks the status of PIND to see if Pin 2 has changed.
​Debouncing Strategy: 1.  Detect a "Falling Edge" (when the button is pressed and the signal drops from 5V to 0V).
2.  Wait for 50ms using _delay_ms(50).
3.  Re-check the pin. If it is still Low, it confirms a real press and not electrical noise.
4.  Increment the count variable and print it.
​### 4. How the System Works (Step-by-Step)
​The system initializes the UART communication so it can "talk" to your computer.
​The program enters an infinite while(1) loop.
​When you press the button, the logic detects the change.
​The "Debounce" delay runs to filter out mechanical vibration.
​The screen displays: Counter: 1, Counter: 2, and so on.

​


## Task 2: Home Automation System via Bluetooth (AVR C)
​### Project Overview
​This project implements a wireless Home Automation system using the ATmega328P microcontroller. The system allows for remote control of electrical appliances (represented by an LED) using a smartphone application and an HC-05 Bluetooth Module.
​Unlike standard Arduino libraries, this project uses Register-Level Programming (AVR C) to manage UART communication and GPIO, ensuring high performance and efficient memory usage.
​### Technical Working Logic
​The system operates on Asynchronous Serial Communication:
​Baud Rate Configuration: The system is set to 9600 bps by calculating the UBRR0 (USART Baud Rate Register) based on a 16MHz CPU frequency.
​Wireless Reception: The smartphone app sends ASCII characters ('1' or '0') via Bluetooth to the HC-05 module.
​UART Reception: The UART_receive() function polls the RXC0 (USART Receive Complete) flag. Once data is available, it is read from the UDR0 register.
​Hardware Action:
​Receiving '1': The bit PB5 in the PORTB register is set high, turning the LED ON.
​Receiving '0': The bit PB5 in the PORTB register is cleared, turning the LED OFF.
### Hardware & Software Requirements
​Microcontroller: Arduino Uno (ATmega328P).
​Communication: HC-05 Bluetooth Module.
​Programming Language: AVR C (Embedded C).
​Compiler: AVR-GCC / Tinkercad Simulator.





## Task 3: Temperature Monitoring System (AVR C)
​### Project Overview
​This project involves designing an embedded system to measure and display real-time ambient temperature. Using an ATmega328P (Arduino Uno), the system interfaces with a TMP36 Analog Temperature Sensor.
​The project is implemented using AVR Register-Level Programming, specifically utilizing the Analog-to-Digital Converter (ADC) and USART (UART) modules to process sensor data and transmit it to a Serial Monitor without the use of high-level Arduino libraries.
​### Technical Working Logic
​The system follows a three-step process: Sensing, Conversion, and Transmission.
​Analog Sensing: The TMP36 sensor outputs a voltage linearly proportional to the Celsius temperature.
​ADC Configuration: * The ADMUX register is configured to use AVcc (5V) as the reference voltage.
​The ADCSRA register is used to enable the ADC and set a prescaler of 128 (converting the 16MHz clock to a stable 125kHz for sampling).
​Data is read from the A0 (ADC0) pin.
​Data Processing: * The 10-bit digital value (0 to 1023) is converted back to voltage.
​Formula: Celsius = \frac{ADC \times 5.0 \times 100.0}{1024.0}
​The dtostrf() function is used to convert the float temperature value into a string for serial transmission.
​UART Transmission: The processed string is sent to the Serial Monitor via the UDR0 register at a baud rate of 9600.

Component      Sensor Pin      Arduino Pin      Register/Port
TMP36 Sensor   Power (VCC)      5V                 VCC
TMP36 Sensor   Ground (GND)     GND                GND
TMP36 Sensor   Vout (Signal)    A0                 ADC0

### Hardware & Software Requirements
​Microcontroller: Arduino Uno (ATmega328P).
​Sensor: TMP36 Precision Temperature Sensor.
​Communication: USB-Serial (UART).
​Programming: AVR C (Embedded C).
​Simulation: Tinkercad.






