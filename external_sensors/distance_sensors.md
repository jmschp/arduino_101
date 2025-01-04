# Sensing distance

- [Sensing distance](#sensing-distance)
  - [Sensing distance with the Ultrasonic Ranging Module HC-SR04](#sensing-distance-with-the-ultrasonic-ranging-module-hc-sr04)

## Sensing distance with the Ultrasonic Ranging Module HC-SR04

We can use a [Ultrasound](https://en.wikipedia.org/wiki/Ultrasound) to measure a distance of an object. For this experiment I am using the [HC-SR04](https://docs.google.com/document/d/1Y-yZnNhMYy7rwhAgyL_pfa39RsB-x2qR4vP8saG73rE/edit). The HC-SR04 has 2 [Ultrasonic transducers](https://en.wikipedia.org/wiki/Ultrasonic_transducer), one transmitter and one receiver.

Specification:

- Detecting range: 3 cm - 400 cm
- Resolution 1 cm
- Best in 30 degree angle
- 5VDC power supply
- Global Current Consumption 15 mA
- Dual transducer
- Ultrasonic Frequency 40k Hz
- Trigger Pulse Width 10 μs

The HC-SR04 as 4 pins 2 for power (Vcc and GND), and another 2 for Trigger an Echo. A device such as the Arduino using this sensor will issue a ping through the Trigger, effectively emitting a Ultrasound, and when the sensor receives the Echo of the Ultrasound will set to HIGH the Echo pin. The distance of the object can be calculated based on the time between sending and receiving.

![HC-SR04 sens0r Arduino schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0510%20-%20Ultrasonic%20distance%20sensor/0510%20-%20Ultrasonic%20Sensor%20HC-SR04.png?raw=true) "HC-SR04 sens0r Arduino schematics"

In the following sketch we use the HC-SR04 to measure the distance of an object. And we rely in the [speed of Sound](https://en.wikipedia.org/wiki/Speed_of_sound) to achieve our distance calculation, the time it takes the ultrasound to reach the object and return. The Speed of Sound at room temperature (20°C) is about 343 m/s.

$$
343 m/s \Leftrightarrow 34300 cm/s \Leftrightarrow 0.0343 cm/μs \\
\text{we can convert that to a fraction}\\
\frac{343}{10000}cm/μs \Leftrightarrow \frac{1}{29,15451895}cm/μs
$$

We can calculate the distance dividing the duration of the signal by 2 (because we only care about the the returning duration, and not the total round trip), and then dividing again by 29,15451895.

$$
distance = \frac{\frac{duration}{2}}{29,15451895} cm
$$

The sketch works as follows:

1. In the setup we initialize Digital Pin 2 as Trigger and Digital Pin 4 as Echo.
2. In the loop we start by setting Trigger to LOW for just 2 microseconds
3. Then we set the Trigger HIGH and back to LOW for 10 microseconds
4. With the `pulseIn` we measure the time that the Echo Pin went form LOW to HIGH and back to LOW
5. This will give us the duration, the time it took since sending the signal and receiving it.
6. Finally apply the above formula

```c++
#define trigPin 2
#define echoPin 4

void setup() {
  Serial.begin (9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  long duration, distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = (duration / 2) / 29.155;

  if (distance >= 400 || distance <= 0){
    Serial.println("Out of range");
  }
  else {
    Serial.print(distance);
    Serial.println(" cm");
  }
  delay(500);
}
```
