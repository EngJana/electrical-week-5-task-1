# electrical-week-5-task-1

smart methods internship week 5 task 1: ESP32 Motion-Activated LED with LDR and PIR

This project demonstrates how to use an ESP32 to control an LED using a relay module based on inputs from a Light Dependent Resistor (LDR) and a Passive Infrared (PIR) motion sensor. The LED will turn on when the ambient light is below a certain threshold and motion is detected.

## Components
- ESP32 Development Board
- Light Dependent Resistor (LDR)
- PIR Motion Sensor
- Relay Module (5V or 3.3V, depending on your ESP32's capabilities)
- LED
- 220-ohm Resistor
- 10k-ohm Resistor
- Breadboard
- Jumper Wires

## Circuit Diagram

Below is the circuit diagram for the project:

<img width="322" alt="u" src="https://github.com/user-attachments/assets/f5e04b1e-f726-4f0c-9762-c8a3a125d89a">

### Connections

**LDR:**
1. Connect one leg of the LDR to the 3.3V pin on the ESP32.
2. Connect the other leg of the LDR to GPIO 14 on the ESP32.
3. Connect one end of a 10k-ohm resistor to the same leg of the LDR that goes to GPIO 14.
4. Connect the other end of the 10k-ohm resistor to GND.

**PIR Sensor:**
1. Connect the VCC pin of the PIR sensor to the 3.3V pin on the ESP32.
2. Connect the GND pin of the PIR sensor to GND on the ESP32.
3. Connect the OUT pin of the PIR sensor to GPIO 25 on the ESP32.

**Relay Module:**
1. Connect the VCC pin of the relay module to the 3.3V pin on the ESP32.
2. Connect the GND pin of the relay module to GND on the ESP32.
3. Connect the IN pin of the relay module to GPIO 23 on the ESP32.

**LED:**
1. Connect the anode (longer leg) of the LED to the NO (Normally Open) terminal of the relay.
2. Connect the cathode (shorter leg) of the LED to one end of a 220-ohm resistor.
3. Connect the other end of the 220-ohm resistor to GND.

## How It Works

- LDR (Light Dependent Resistor): Detects the ambient light level. When light falls on the LDR, its resistance decreases, resulting in a higher voltage drop across it. This change in resistance is read by the ESP32's analog input pin (GPIO 14).
- PIR (Passive Infrared) Sensor: Detects motion by measuring changes in infrared radiation in its surroundings. When motion is detected, the PIR sensor outputs a HIGH signal to GPIO 25 of the ESP32.
- Relay Module: Acts as a switch to control the LED. When the relay is activated, it closes the circuit between the NO and COM terminals, allowing current to flow through the LED and turn it on.

### Code Explanation

the code is provided in the repositry 

1. **Setup Function**:
- setup() is a function that runs once when the microcontroller is powered on or reset.
Serial.begin(115200) initializes serial communication at a baud rate of 115200 bits per second. This is useful for debugging and monitoring the sensor readings.
- pinMode(ldrPin, INPUT), pinMode(pirPin, INPUT), and pinMode(relayPin, OUTPUT) set the modes of the pins. The LDR and PIR sensor pins are set as inputs, while the relay pin is set as an output.

2. **Loop Function**:
- loop() is a function that runs repeatedly after the setup() function.
- int ldrValue = analogRead(ldrPin) reads the analog value from the LDR pin. This value ranges from 0 to 4095 (since the ESP32 has a 12-bit ADC).
- int pirState = digitalRead(pirPin) reads the digital value from the PIR sensor pin. This value is either HIGH (motion detected) or LOW (no motion detected).
- Serial.print("LDR Value: ") and Serial.println(ldrValue) print the LDR value to the serial monitor for debugging.
- Serial.print("PIR State: ") and Serial.println(pirState) print the PIR sensor state to the serial monitor for debugging.
- if (ldrValue < 2000 && pirState == HIGH) checks if the LDR value is below 2000 (indicating low ambient light) and if the PIR sensor is HIGH (indicating motion detected).
   - If both conditions are met, digitalWrite(relayPin, HIGH) turns on the relay, and Serial.println("Relay ON") prints "Relay ON" to the serial monitor.
   - If either condition is not met, digitalWrite(relayPin, LOW) turns off the relay, and Serial.println("Relay OFF") prints "Relay OFF" to the serial monitor.
- delay(1000) pauses the program for 1 second before repeating the loop.
