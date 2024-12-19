# dracaena-ino
arduino code to remind me to water my Dracaena plant 
-reminder to put photo here of dracaena

## Project Concept
Was worried about not watering my Dracaena plant enough during winter (with heating on), so I created a small system that monitors soil moisture and humidity using the Water Level Detection Sensor (repurposed here to measure soil moisture indirectly) and the DHT11 sensor for ambient humidity. If the soil moisture is too low and ambient humidity is also low, it will display a reminder on the LCD and activate a buzzer alert after a certain threshold. This will let me know when it might be time to water your Dracaena. In the future I think it would be cool to link the board with Apple HomeKit (Matter) to remind me by sending me a push notification to my phone - or when I'm connected (Bluetooth to the sensor) it can show me a live monitor feed of the water level/humidity and all

### Components Needed:

- Arduino Uno - im using an Arduino Mega 2560 R3
- LCD1602 with Pin Header
- Water Level Detection Sensor Module
- DHT11 Temperature & Humidity Module
- Passive Buzzer (to play a tone) or Active Buzzer (simpler beep) - remove this if you dont want an invasive noise - might also be energy efficient to not have something buzzing constantly - might code it to beep as often as smoke detectors do when the battery is out
- A 10K resistor (if needed for LCD contrast or pull-up)
- Jumper Wires
- Breadboard
- USB Cable for power and programming

### Wiring Guide:

*DHT11 Sensor* - DHT11 has three pins: + (Vcc), Out (Signal), GND. Connect + to 5V, GND to Arduino GND, and Out to a digital pin (e.g., D2).

*Water Level Detection Sensor* - The sensor typically has three pins: + (Vcc), S (Signal), (GND). Connect + to 5V, G to GND, S (Signal) to an analog input (e.g., A0 on Arduino).

```bash
Note: You can carefully insert the sensor prongs into the soil to measure soil moisture with a water level sensor. It won’t give an exact soil moisture percentage, but the analog reading will decrease when the soil is drier and increase when damp.
```

*LCD1602 Display*

```bash
Assuming a direct connection (no I2C adapter):

VSS -> GND
VDD -> 5V
VO -> Middle pin of a 10K potentiometer (to adjust contrast), other pot pins to 5V and GND.
RS -> D7 (for example)
E -> D8
D4 -> D9
D5 -> D10
D6 -> D11
D7 -> D12
RW -> GND
A (LED+) -> 5V (with a current limiting resistor ~220Ω)
K (LED-) -> GND
(You can change pins, just be sure to match them in code.)
```

*Buzzer (Active or Passive)* - Active buzzer: Just needs a digital pin and GND. For example:
pin of buzzer -> D5 via a small resistor (220Ω), pin of buzzer -> GND.
If passive: same connection, use tone() function to generate sound.

### Power Up:
Connect Arduino to PC via USB for power and programming.

```bash
DHT11 Library: Use the popular DHT library.
Reading DHT11: Use dht.readHumidity() and dht.readTemperature().
Reading Water Sensor: Use analogRead(A0) to get a value from 0 to 1023. Higher value = more moisture, lower value = drier.
Display on LCD: Initialize the LCD, print messages about humidity and soil moisture.
Trigger Condition: If soil moisture is below a certain threshold and humidity is low, display a reminder and beep the buzzer - might beep the buzzer as frequently as smoke detectors do.
```
