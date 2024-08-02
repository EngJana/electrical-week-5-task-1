# electrical-week-5-task-1

smart methods internship week 5 task 1: ESP32 Motion-Activated LED with LDR

This project demonstrates how to use an ESP32 microcontroller to control an LED based on readings from a Light Dependent Resistor (LDR) and a Passive Infrared (PIR) motion sensor. When the environment is dark and motion is detected, the LED will turn on.

## Components

- ESP32 Development Board
- Light Dependent Resistor (LDR)
- PIR Motion Sensor
- LED
- 220-ohm Resistor
- 10k-ohm Resistor
- Breadboard
- Jumper Wires

## Circuit Diagram

Below is the circuit diagram for the project:

<img width="233" alt="q" src="https://github.com/user-attachments/assets/f5330a29-78a1-45a6-aada-8f04dfdb8587">

### Connections

1. **LDR**:
   - Connect one leg to 3.3V.
   - Connect the other leg to GPIO 14 and one end of a 10k-ohm resistor.
   - Connect the other end of the resistor to GND.

2. **PIR Sensor**:
   - VCC to 3.3V.
   - GND to GND.
   - OUT to GPIO 25.

3. **LED**:
   - Connect the anode (longer leg) to GPIO 23 through a 220-ohm resistor.
   - Connect the cathode (shorter leg) to GND.

## How It Works

### Setup
the code is provided in the repositry 

1. **LDR (Light Dependent Resistor)**:
   - The LDR is used to detect the ambient light level. When light falls on the LDR, its resistance decreases, resulting in a higher voltage drop across it.
   - This changing resistance is converted into a voltage that can be read by the ESP32's analog input pin (GPIO 14).

2. **PIR (Passive Infrared) Sensor**:
   - The PIR sensor detects motion by measuring changes in infrared radiation in its surroundings.
   - When motion is detected, the PIR sensor outputs a HIGH signal to GPIO 25 of the ESP32.

3. **LED**:
   - The LED is connected to GPIO 23 through a 220-ohm resistor to limit the current and prevent damage to the LED.
   - The LED will be controlled based on the readings from the LDR and PIR sensor.

### Code Explanation

1. **Setup Function**:
   - `pinMode()` is used to set the LDR pin (GPIO 14) and PIR pin (GPIO 25) as inputs, and the LED pin (GPIO 23) as an output.
   - `Serial.begin(115200)` initializes serial communication at a baud rate of 115200 for debugging.

2. **Loop Function**:
   - **Reading Sensor Values**:
     - `ldrValue = analogRead(ldrPin)` reads the analog value from the LDR. This value ranges from 0 to 4095 on the ESP32.
     - `pirState = digitalRead(pirPin)` reads the digital value from the PIR sensor (HIGH if motion is detected, LOW otherwise).

   - **Debugging**:
     - The LDR and PIR values are printed to the serial monitor for debugging purposes.
     - Conditional statements print whether the environment is dark or bright and whether motion is detected.

   - **LED Control Logic**:
     - If the LDR value is less than 2000 (indicating darkness) and the PIR sensor detects motion (HIGH), the LED is turned on using `digitalWrite(ledPin, HIGH)`.
     - If either the environment is not dark or no motion is detected, the LED is turned off using `digitalWrite(ledPin, LOW)`.

   - **Delay**:
     - `delay(1000)` introduces a delay of 1 second between each loop iteration to avoid flooding the serial monitor with too many messages.

