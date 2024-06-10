# Prototyping

- [Prototyping](#prototyping)
  - [Breadboards](#breadboards)
  - [Jumper wires](#jumper-wires)
  - [Multimeter](#multimeter)
    - [Using a Multimeter Measuring Voltage (V)](#using-a-multimeter-measuring-voltage-v)
    - [Using a Multimeter Measuring Current (A)](#using-a-multimeter-measuring-current-a)
    - [Using a Multimeter Measuring Resistance (Ω)](#using-a-multimeter-measuring-resistance-ω)
    - [Using a Multimeter Measuring Testing Continuity](#using-a-multimeter-measuring-testing-continuity)
  - [Soldering](#soldering)
  - [Simple external sensors](#simple-external-sensors)
    - [Light-emitting diode (LED)](#light-emitting-diode-led)
    - [Button](#button)
    - [Potentiometer](#potentiometer)
    - [Photoresistor](#photoresistor)

## Breadboards

Breadboards are used to prototyping a circuit. In the following breadboard we have 4 set of columns:

- One set labeled **a b c d e**, within this set each row 1 to 30 is connected horizontally. So something we plug in a1 it will be connected to something connected in e1, but is is not connected to something in any of the other rows, unless we use a jumper wire to connect different rows.
- Another set labeled **f g h i f** works in the same way, as the above.
- Then we have in each extremity 2 columns labeled **+** (positive) and **-** (negative). These are connected vertically.

![Breadboard](./images/breadboard.jpg "Breadboard")

The following GIF from Adafruit show how are the breadboards connected.

![Adafruit breadboard GIF](https://cdn-learn.adafruit.com/assets/assets/000/035/419/original/components_halfbb.gif "Adafruit breadboard GIF")

- [Adafruit Breadboards](https://learn.adafruit.com/breadboards-for-beginners/breadboards)
- [Wikipedia Breadboard](https://en.wikipedia.org/wiki/Breadboard)

## Jumper wires

We have several types of jumper wires, I list some of the most commons below, although there are several others.

Jumper wires male to male

![Jumper wires male to male](./images/jumper_wires_mate_male.jpg "Jumper wires male to male")

Jumper wires male to female

![Jumper wires male to female](./images/jumper_wires_mate_female.jpg "Jumper wires male to female")

Jumper wires female to female

![Jumper wires female to female](./images/jumper_wires_femate_female.jpeg "Jumper wires female to female")

Jumper wires crocodile clip

![Jumper wires crocodile clip](./images/jumper_wires_crocodile_clip.jpg "Jumper wires crocodile clip")

## Multimeter

The most common measures we will need are:

<!-- markdownlint-disable MD033 -->

- Voltage: V
  - AC Voltage: V<sup>~</sup>
  - DC Voltage: V<sup>⎓</sup>
  - AC/DC Voltage V<sup>≂</sup>
  - AC/DC milliVolts mV<sup>≂</sup>
- Current: Amperage A
  - AC Amperage A<sup>~</sup>
  - AC Amperage A<sup>⎓</sup>
  - AC/DC Amperage A<sup>≂</sup>
- Resistance: Ω
- Continuity: `)))))`

Components of a Multimeter:

- Display: Shows the measurement readings.
- Selection Dial: Allows you to choose the type of measurement (voltage, current, resistance, continuity).
- Probes: Red (positive) and black (negative) probes are used to make contact with the circuit.
- Ports: Different input ports for the probes, usually marked COM (common/ground), VΩ (voltage/resistance), and mA/10A (current).

Some, more simple, multimeters do not have auto-ranging feature, so first we need to determine the expected voltage before the measurement. Such multimeters usually have the following modes available (here considering V<sup>⎓</sup>, actual ranges vary from model to model):

- 200mV<sup>⎓</sup> -> the expected Voltage is between 0 Volts and 200 milliVolts
- 2000mV<sup>⎓</sup> -> the expected Voltage is between 200 milliVolts and 2000 milliVolts
- 20V<sup>⎓</sup> -> the expected Voltage is between 2000 milliVolts and 20 Volts
- 200V<sup>⎓</sup> -> the expected Voltage is between 20 Volts and 200 Volts
- 500V<sup>⎓</sup> -> the expected Voltage is between 200 Volts and 500 Volts

In such a multimeter, if we are expecting a Voltage of 5V, we should set the multimeter to measure up to 20V. The same principle applies when measuring Current (A), although in this case, if we measure a higher value than the selected range we can burn a fuse of the multimeter. In either case always start with the highest range when uncertain.

### Using a Multimeter Measuring Voltage (V)

There are two types fo Voltage Measurement:

- DC Voltage (V with straight line Voltage: V<sup>⎓</sup>): For batteries, DC power supplies.
- AC Voltage (V with wavy line: V<sup>~</sup>): For mains electricity, like a socket at home.

Steps:

- Set the Dial: Turn the dial to the appropriate voltage type (V⎓ for DC, V~ for AC).
- Connect Probes:
  - Black probe to **COM** port.
  - Red probe to **VΩ** port.
- Measure:
  - Touch the black probe to the negative side (or ground) of the circuit.
  - Touch the red probe to the positive side of the component or circuit.
  - Read the voltage on the display.

### Using a Multimeter Measuring Current (A)

there are two types of Current Measurement:

- DC Current (A with straight line: A<sup>~</sup>). For batteries, DC power supplies.
- AC Current (A with wavy line: A<sup>⎓</sup>). For mains electricity, like a socket at home.
<!-- markdownlint-enable MD033 -->

Steps:

- Set the Dial: Turn the dial to the appropriate current type and range (often A⎓ for DC current).
- Connect Probes:
  - Black probe to **COM** port.
  - Red probe to the **mA** port for small currents or **10A** port for larger currents. Some multimeters have a single port **mA/A**
- Measure:
  - Break the circuit where we want to measure the current.
  - Insert the multimeter in series with the circuit (current flows through the multimeter).
  - Read the current on the display.

Note: Always start with the highest range to avoid damaging the multimeter, then switch to lower ranges as needed.

### Using a Multimeter Measuring Resistance (Ω)

With this setting we can measure resistance in a circuit. We could use to measure the resistance in a Resistor, for example.

Steps:

- Set the Dial: Turn the dial to the resistance measurement (Ω symbol).
- Connect Probes:
  - Black probe to **COM** port.
  - Red probe to **VΩ** port.
- Measure:
  - Ensure the circuit is powered off (no voltage).
  - Touch the probes to either side of the component whose resistance we want to measure.
  - Read the resistance on the display.

Note: If measuring a component in-circuit, ensure there's no parallel path that could affect the reading.

### Using a Multimeter Measuring Testing Continuity

Steps:

- Set the Dial: Turn the dial to the continuity test mode (diode symbol or sound wave symbol).
- Connect Probes:
  - Black probe to COM port.
  - Red probe to VΩ port.
- Measure:
  - Touch the probes to both ends of the wire, trace, or component we want to test.
  - If there is continuity (a complete path), the multimeter will beep (depending on model).

![Multimeter](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/2017_Cyfrowy_miernik_uniwersalny.jpg/1600px-2017_Cyfrowy_miernik_uniwersalny.jpg?20180731085219 "Multimeter")

- [Wikipedia Multimeter](https://en.wikipedia.org/wiki/Multimeter)
- [Electric current](https://en.wikipedia.org/wiki/Electric_current)
- [Ammeter](https://en.wikipedia.org/wiki/Ammeter)
- [Adafruit Multimeter](https://learn.adafruit.com/multimeters)

## Soldering

- [Wikipedia Solder](https://en.wikipedia.org/wiki/Solder)
- [Sciences at Smith College - The Basic Soldering Guide](https://www.science.smith.edu/~jcardell/Courses/EGR328/Readings/Soldering%20Guide.pdf)
- [Adafruit Guide To Excellent Soldering](https://learn.adafruit.com/adafruit-guide-excellent-soldering)

## Simple external sensors

### Light-emitting diode (LED)

> A light-emitting diode (LED) is a semiconductor device that emits light when current flows through it. Electrons in the semiconductor recombine with electron holes, releasing energy in the form of photons. The color of the light (corresponding to the energy of the photons) is determined by the energy required for electrons to cross the band gap of the semiconductor.

[Wikipedia Light-emitting diode](https://en.wikipedia.org/wiki/Light-emitting_diode)

Single color LEDs have an anode and a cathode, while multiple color LEDs have one terminal for each color, the most common are RGB LEDs, which have 3 terminals, for each color (red, green and blue), and a forth terminal, which either is the common anode or cathode. For standard 5mm diameter LEDs the maximum current is usually 20mA.

![Tinkercad LEDs and RGB LED](./images/led_rgb_led.png "Tinkercad LEDs and RGB LED")

[Tinkercad LEDs and RGB LED](https://www.tinkercad.com/things/7xL8Mb6K1Eo-led-and-rgb-led)

### Button

> A push-button (also spelled pushbutton) or simply button is a simple switch mechanism to control some aspect of a machine or a process. Buttons are typically made out of hard material, usually plastic or metal.

[Wikipedia Push-button](https://en.wikipedia.org/wiki/Push-button)

In the following circuit a push-button controls an LED. If we push the button the LED turns on, release it and it tuns of. This particular button has 4 pins, the 2 pins on the left are. always connected to each other, so it's basically the same pin. The same happens to the pins on the right.

![LED Push-button circuit](./images/push-button_led.png "LED Push-button circuit")

[Tinkercad Push-button LED](https://www.tinkercad.com/things/a3ouPZUmi7G-push-button-led)

### Potentiometer

> A potentiometer is a three-terminal resistor with a sliding or rotating contact that forms an adjustable voltage divider.

[Wikipedia Potentiometer](https://en.wikipedia.org/wiki/Potentiometer)

In the following circuit we have a potentiometer controlling an LED. The potentiometer is has 3 pins, the middle pin is the wiper and the and the 2 outside pins one is positive and the other negative. LED and the potentiometer share the same ground, and the anode of the LED is connected to the middle pin (wiper pin) of the potentiometer. If the potentiometer is fully turned anti clockwise the LED is receiving 0V, so is off. The more we turn the potentiometer clockwise more power the LED receives.

![LED Potentiometer LED circuit](./images/potentiometer_led.png "LED Push-button circuit")

[Tinkercad Potentiometer LED](https://www.tinkercad.com/things/1l70Uxi84LY-potentiometer-led)

### Photoresistor

> A photoresistor (also known as a light-dependent resistor, LDR, or photo-conductive cell) is a passive component that decreases in resistance as a result of increasing luminosity (light) on its sensitive surface, in other words, it exhibits photoconductivity.

In other words the more light it receives the less resistance it has, so more current flows through it. They have two, not polarized terminals, just like a fixed resistor.

[Wikipedia Photoresistor](https://en.wikipedia.org/wiki/Photoresistor)

![Photoresistor LED](./images/photoresistor_led.png "Photoresistor LED")

[Tinkercad Photoresistor LED](https://www.tinkercad.com/things/kn5F8VMbdI1-photoresistor-led)
