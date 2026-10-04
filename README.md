# Smart-Security-System
An embedded, hardware-based security system prototype developed on an Arduino Uno R3. The project demonstrates real-time hardware control, analog sensor signal processing, bitwise shift register operation, and modular C++ state machine architecture.

Project Overview:
This security system acts as a light sensing tripwire alarm. It monitors an environment using a photoresistor(LDR) voltage divider circuit. The system processes state changes through physical button inputs, and drives visual and acoustic alerts using a 74HC595 shift register and a Piezo buzzer. The code avoids blockings and delays via delay(), relying on software timers using the function Millis(), which handles the operation of seven LEDs, sensor programing, and audio genration. 

System Architecture & Engineering Highlights:
1. Non-Blocking Finite State Machine
   The firmware contains three functional states:
   - Disarmed State: The system is powered off. Sensors, alarms, and LEDs remain deactviated. Howver the pushbutton is contasntly on stand by to detect input.
     - Armed State: This state is activate by pressing the pushbutton. Upon pressing the pushbutton a blue LED will illuminate signaling that the system is sensing LDR brightness.
     - Triggered State: This state is activated when the light level below the calibrated analog threshold of less than 900. This than triggers the Piezo which simultaneously dispenses audio coordinating with the LEDs which illuminate in a rotational manner.
2. Shift registor pin Expansion:
   To conserve pin on the Arduino, the seven LEDs are controlled via a 74HC595 serial in parrelel out shift registor.
   - The shift register consist of three functions, Data(DS), Clock(SH_CP), and Latch(ST_CP)
   - The shift registor uses bitwise shift operators (<<) to shift binary patterns between the LEDs allowing them to illuminate in a rotational manner.
3. Analog Signal Conditioning
   - The LDR is configured in a voltage divider network paired with a $10\text{k}\Omega$ resistor.
   - Analog values are sampled continuously using analogRead(), comparing the input voltage against a calibrated threshold to detect optical beam interruptions.

Materials Used: 
- 1 Arduino Uno R3
- 1 74HC595 Integrated Circuit
- 1 Light Dependent Resistor or Photoresistor
- 1 Piezo Buzzer
- 1 Push button
- 7 LEDs
- 7 220K ohm resistors
- 1 10K ohm resistor
- 1 small breadboard
- Jumper wires

Hardware Wiring & Pin Mapping:
Shift registor(74HC595) to microcontroller:
- Data pin 14: Arduino Digital pin 11
- Latch Pin (ST_CP / Pin 12): Arduino Digital Pin 12
- Clock Pin (SH_CP / Pin 11): Arduino Digital Pin 13
- Output Enable pin 13 to ground
- Master reset pin 10 to 5V
Sensors & Actuators:
- LDR Signal Pin: Arduino Analog Pin A0 in series with the 10K ohm resistor connected ot ground
- Pushbutton Pin: Arduino Digital Pin 2
- Piezo Buzzer: Arduino Digital Pin 3

**Getting Started **
- Wire the components according to the pin mapping table above.
- Ensure common ground (GND) across the Arduino, breadboard rails, and 74HC595 IC.

**Firmware Operations on Arduino IDE:**
- Open firmware/security_system.ino in the Arduino IDE.
- Select Tools, Board, than Ardunio Uno
- Select your serial port and click Upload.
- Open the Serial Monitor at 9600 baud to observe live LDR ADC values and state transitions.

