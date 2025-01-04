# Detecting objects with Passive Infrared sensor (PIR)

- [Detecting objects with Passive Infrared sensor (PIR)](#detecting-objects-with-passive-infrared-sensor-pir)
  - [Detecting objects with HC-SR501 PIR](#detecting-objects-with-hc-sr501-pir)
    - [Using a HC-SR501 PIR sensor to interact with an LED](#using-a-hc-sr501-pir-sensor-to-interact-with-an-led)

> A passive infrared sensor (PIR sensor) is an electronic sensor that measures infrared (IR) light radiating from objects in its field of view. They are most often used in PIR-based motion detectors. PIR sensors are commonly used in security alarms and automatic lighting applications.

[Wikipedia Passive infrared sensor](https://en.wikipedia.org/wiki/Passive_infrared_sensor)

Any object with a temperature above [absolute zero](https://en.wikipedia.org/wiki/Absolute_zero) emits heat energy in the form of electromagnetic radiation. This radiation can be detected by the PIR sensor.

## Detecting objects with HC-SR501 PIR

The [HC-SR501](https://www.epitran.it/ebayDrive/datasheet/44.pdf) is digital PIR sensor, that provides several adjustments.

- **Time Delay Adjust**: Sets how long the output remains high after detecting motion. Anywhere from 5 seconds to 5minutes.
- **Sensitivity Adjust**: Sets the detection range from 3 meters to 7 meters.
- **Trigger Selection Jumper**: Set for single or repeatable triggers.
  - **H** mode: repeat trigger. Sensor output is high for as long there is movement in front of sensor.
  - **L** mode: single trigger. Sensor output is high for a short period of time (determined by delay time adjustment), then it goes low, even if there is movement in front of the sensor. Output will go high again, if detects motion, after about 3 seconds.

We can use the sensor with a simple battery, to interact with an LED.

![PIR and LED with battery schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0500%20-%20Infrared%20motion%20sensor/0500%20-%20Infrared%20sensor.png?raw=true "PIR and LED with battery schematics")

[Tinkercad PIR and LED with battery](https://www.tinkercad.com/things/fpPOaKOp94J-passive-infrared-sensor-led-battery).

Or we can use it with the Arduino, reading the sensor output in an Arduino's digital input.

![PIR and LED with Arduino schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0500%20-%20Infrared%20motion%20sensor/0500%20-%20Infrared%20sensor%20with%20Arduino.png?raw=true "PIR and LED with Arduino schematics")

[Tinkercad PIR and LED with Arduino](https://www.tinkercad.com/things/cVIg5B548y1-passive-infrared-sensor-led).

### Using a HC-SR501 PIR sensor to interact with an LED

In the following sketch we use the output form the PIR sensor as input for a LED. In the setup we set the desired pin modes, and we wait for 1 minute for the sensor to initialize (it is the recommended time for the HC-SR501 sensor). Then in the loop, we just read the PIR sensor value and pass it to the LED.

```c++
const int pirInputPin = 7;
const int ledOutputPin = 8;

void setup() {
  pinMode(7, INPUT);
  pinMode(8, OUTPUT);
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(115200);
  while (!Serial) {
    ;  // wait for serial port to connect. Needed for native USB
  }
  Serial.println("Initializing sensor. Wait 1 minute");
  digitalWrite(LED_BUILTIN, HIGH);
  delay(60000);
  digitalWrite(LED_BUILTIN, LOW);
  Serial.println("Sensor initialized.");
}

void loop() {
  int pirValue = digitalRead(pirInputPin);
  Serial.println(pirValue);
  digitalWrite(ledOutputPin, pirValue);
}
```
