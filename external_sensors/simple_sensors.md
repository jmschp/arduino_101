# Simple sensors

- [Simple sensors](#simple-sensors)
  - [Light-emitting diode (LED)](#light-emitting-diode-led)
  - [Push-button](#push-button)
  - [Potentiometer](#potentiometer)
  - [Sample sketches with external sensors](#sample-sketches-with-external-sensors)
    - [Controlling an LED with a push-button (pull-down resistor)](#controlling-an-led-with-a-push-button-pull-down-resistor)
    - [Using 3 potentiometer to control and RGB LED](#using-3-potentiometer-to-control-and-rgb-led)

## Light-emitting diode (LED)

> A light-emitting diode (LED) is a semiconductor device that emits light when current flows through it. Electrons in the semiconductor recombine with electron holes, releasing energy in the form of photons. The color of the light (corresponding to the energy of the photons) is determined by the energy required for electrons to cross the band gap of the semiconductor.

[Wikipedia Light-emitting diode](https://en.wikipedia.org/wiki/Light-emitting_diode)

Single color LEDs have an anode and a cathode, while multiple color LEDs have one terminal for each color, the most common are RGB LEDs, which have 3 terminals, for each color (red, green and blue), and a forth terminal, which either is the common anode or cathode. For standard 5mm diameter LEDs the maximum current is usually 20mA.

![Tinkercad LEDs and RGB LED](../images/led_rgb_led.png "Tinkercad LEDs and RGB LED")

[Tinkercad LEDs and RGB LED](https://www.tinkercad.com/things/7xL8Mb6K1Eo-led-and-rgb-led)

## Push-button

> A push-button (also spelled pushbutton) or simply button is a simple switch mechanism to control some aspect of a machine or a process. Buttons are typically made out of hard material, usually plastic or metal.

[Wikipedia Push-button](https://en.wikipedia.org/wiki/Push-button)

In the following circuit a push-button controls an LED. If we push the button the LED turns on, release it and it tuns of. This particular button has 4 pins, the 2 pins on the left are. always connected to each other, so it's basically the same pin. The same happens to the pins on the right.

![LED Push-button circuit](../images/push-button_led.png "LED Push-button circuit")

[Tinkercad Push-button LED](https://www.tinkercad.com/things/a3ouPZUmi7G-push-button-led)

## Potentiometer

> A potentiometer is a three-terminal resistor with a sliding or rotating contact that forms an adjustable voltage divider.

[Wikipedia Potentiometer](https://en.wikipedia.org/wiki/Potentiometer)

[Basics of Potentiometers with Arduino](https://docs.arduino.cc/learn/electronics/potentiometer-basics/)

In the following circuit we have a potentiometer controlling an LED. The potentiometer is has 3 pins, the middle pin is the wiper and the and the 2 outside pins one is positive and the other negative. LED and the potentiometer share the same ground, and the anode of the LED is connected to the middle pin (wiper pin) of the potentiometer. If the potentiometer is fully turned anti clockwise the LED is receiving 0V, so is off. The more we turn the potentiometer clockwise more power the LED receives.

![LED Potentiometer LED circuit](../images/potentiometer_led.png "LED Push-button circuit")

[Tinkercad Potentiometer LED](https://www.tinkercad.com/things/1l70Uxi84LY-potentiometer-led)

## Sample sketches with external sensors

### Controlling an LED with a push-button (pull-down resistor)

We set Digital Pin 7 as output for the LED, and Digital Pin 5 as input from the push-button.

```c++
const int ledOutputPin = 7;
const int buttonInputPin = 5;

void setup() {
  pinMode(buttonInputPin, INPUT);
  pinMode(ledOutputPin, OUTPUT);
}

void loop() {
  digitalWrite(ledOutputPin, digitalRead(buttonInputPin));
}
```

[Tinkercad Digital Input Button Pull Down Resistor](https://www.tinkercad.com/things/doukbpoqPSL-digital-input-button-pull-down-resistor)

### Using 3 potentiometer to control and RGB LED

In the global scope we first assign constants to each pin we need. Pins A0, A1 and A2 will be the analog inputs from the potentiometers wipers, then Digital Pins 3, 5, 6, will act as PWM pins for output to the RGB LED.

In the `loop` we read what is the value of each potentiometer, with `analogRead`, then `map` the value, which is an integer from 0 to 1023, to the value supported by the PWM pins, which is between 0 and 255. Finally we output the read value to each color pin of the RGB LED with `analogWrite`.

```c++
const int redPotentiometerPin = A0;
const int greenPotentiometerPin = A1;
const int bluePotentiometerPin = A2;

const int redLedPin = 3;
const int greenLedPin = 5;
const int blueLedPin = 6;

void setup() {
  pinMode(redLedPin, OUTPUT);
  pinMode(greenLedPin, OUTPUT);
  pinMode(blueLedPin, OUTPUT);
}

void loop() {
  int redPotentiometerVal = analogRead(redPotentiometerPin);
  int greenPotentiometerVal = analogRead(greenPotentiometerPin);
  int bluePotentiometerVal = analogRead(bluePotentiometerPin);

  long redLedVal = map(redPotentiometerVal, 0, 1023, 0, 255);
  long greenLedVal = map(greenPotentiometerVal, 0, 1023, 0, 255);
  long blueLedVal = map(bluePotentiometerVal, 0, 1023, 0, 255);

  analogWrite(redLedPin, redLedVal);
  analogWrite(greenLedPin, greenLedVal);
  analogWrite(blueLedPin, blueLedVal);
}
```

[Tinkercad Potentiometers RGB LED](https://www.tinkercad.com/things/blFnvm6MEm5-potentiometers-rgb-led)
