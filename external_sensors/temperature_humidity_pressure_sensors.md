# Temperature, humidity and pressure sensors

- [Temperature, humidity and pressure sensors](#temperature-humidity-and-pressure-sensors)
  - [Measuring temperature and humidity with the DHT22](#measuring-temperature-and-humidity-with-the-dht22)
    - [Using the DHT22 temperature and humidity sensor](#using-the-dht22-temperature-and-humidity-sensor)
  - [Thermistor](#thermistor)
    - [Using the Thermistor to measure temperature](#using-the-thermistor-to-measure-temperature)
  - [Measuring temperature with the TMP36](#measuring-temperature-with-the-tmp36)
    - [Using the TMP36 to measure temperature](#using-the-tmp36-to-measure-temperature)
  - [Measuring temperature with the MCP9808](#measuring-temperature-with-the-mcp9808)
  - [Measuring atmospheric pressure with BMP180](#measuring-atmospheric-pressure-with-bmp180)

## Measuring temperature and humidity with the DHT22

The DHT22 is a digital sensor capable of measuring temperature, within -40º to 80º Celsius and humidity from (0% to 100% RH, it may take up to 5 seconds to take a measurement. With temperature and relative humidity we can calculate the [Heat index](https://en.wikipedia.org/wiki/Heat_index).

The sensor can be power with a 3.3-6V DC power supply. [Full Datasheet](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf).

The sensor comes with either 3 or 4 pins. The ones that have 4 pins means that one of the pins is not connected, usually pin 3. We can connect it to an Arduino, using its 3 pins, one for GND anther for power, and the data pin connected to one of Arduino's digital inputs:

![DHT22 Temperature sensor schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0430%20-%20DHT22/0430%20-%20DHT22.png?raw=true)

Notice the 10kOhm "strong" pull-up resistor. This is implemented this way to avoid a a floating condition in the Arduino digital input, when the sensor is not transmitting any data.

### Using the DHT22 temperature and humidity sensor

To read data from a DHT22, we can use the Adafruit DHT library. The following code is from Adafruit DHT library [example](https://github.com/adafruit/DHT-sensor-library/blob/master/examples/DHTtester/DHTtester.ino).

```c++
#include "DHT.h"

#define DHTPIN 2  // Digital pin connected to the DHT sensor

// Uncomment whatever type you're using!
//#define DHTTYPE DHT11   // DHT 11
#define DHTTYPE DHT22  // DHT 22  (AM2302), AM2321
//#define DHTTYPE DHT21   // DHT 21 (AM2301)


// Initialize DHT sensor.
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  Serial.println(F("DHTxx test!"));

  dht.begin();
}

void loop() {
  // Wait a few seconds between measurements.
  delay(5000);

  // Reading temperature or humidity takes about 250 milliseconds!
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  float h = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float t = dht.readTemperature();
  // Read temperature as Fahrenheit (isFahrenheit = true)
  float f = dht.readTemperature(true);

  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println(F("Failed to read from DHT sensor!"));
    return;
  }

  // Compute heat index in Fahrenheit (the default)
  float hif = dht.computeHeatIndex(f, h);
  // Compute heat index in Celsius (isFahreheit = false)
  float hic = dht.computeHeatIndex(t, h, false);

  Serial.print(F("Humidity: "));
  Serial.print(h);
  Serial.print(F("%  Temperature: "));
  Serial.print(t);
  Serial.print(F("°C "));
  Serial.print(f);
  Serial.print(F("°F  Heat index: "));
  Serial.print(hic);
  Serial.print(F("°C "));
  Serial.print(hif);
  Serial.println(F("°F"));
}
```

## Thermistor

> A thermistor is a semiconductor type of resistor whose resistance is strongly dependent on temperature, more so than in standard resistors.
>
> Depending on materials used, thermistors are classified into two types:
>
> - With NTC (Negative-temperature-coefficient) thermistors, resistance decreases as temperature rises; usually due to an increase in conduction electrons bumped up by thermal agitation from the valence band. An NTC is commonly used as a temperature sensor, or in series with a circuit as an inrush current limiter.
> - With PTC (Positive-temperature-coefficient) thermistors, resistance increases as temperature rises; usually due to increased thermal lattice agitations, particularly those of impurities and imperfections. PTC thermistors are commonly installed in series with a circuit, and used to protect against overcurrent conditions, as resettable fuses.

[Wikipedia Thermistor](https://en.wikipedia.org/wiki/Thermistor)

As with the thermistor, we will need to assemble a voltage divider circuit to use with the Arduino.

![Thermistor Voltage Divider schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0440%20-%20Thermistor/0440%20-%20Thermistor%205V.png?raw=true)

To get the temperature of the thermistor we can use the [Steinhart–Hart equation](https://en.wikipedia.org/wiki/Steinhart%E2%80%93Hart_equation). There are Arduino libraries that implement the equation, for example [panStamp/thermistor](https://github.com/panStamp/thermistor) and [suoapvs/NTC_Thermistor](https://github.com/suoapvs/NTC_Thermistor). The coefficients needed to calculate the temperature can be found in the thermistor Datasheet. The one I am using is [NTC 10KR 500mW Ø6.5mm](https://storage.googleapis.com/mauser-public-images/prod_description_document/2023/3/33f465c10d296f2fff37f6107f732a39_ntcc-10k.pdf).

### Using the Thermistor to measure temperature

In this code I use the [suoapvs/NTC_Thermistor](https://github.com/suoapvs/NTC_Thermistor) to get the thermistor temperature.

```c++
#include <Thermistor.h>
#include <NTC_Thermistor.h>

#define SENSOR_PIN A0
#define REFERENCE_RESISTANCE 9830
#define NOMINAL_RESISTANCE 10000
#define NOMINAL_TEMPERATURE 25
#define B_VALUE 4050

Thermistor* thermistor;

void setup() {
  Serial.begin(9600);

  thermistor = new NTC_Thermistor(
    SENSOR_PIN,
    REFERENCE_RESISTANCE,
    NOMINAL_RESISTANCE,
    NOMINAL_TEMPERATURE,
    B_VALUE);
}


void loop() {
  const double celsius = thermistor->readCelsius();
  const double kelvin = thermistor->readKelvin();
  const double fahrenheit = thermistor->readFahrenheit();

  Serial.print("Temperature: ");
  Serial.print(celsius);
  Serial.print(" C, ");
  Serial.print(kelvin);
  Serial.print(" K, ");
  Serial.print(fahrenheit);
  Serial.println(" F");

  delay(2000);
}
```

## Measuring temperature with the TMP36

The TMP36 is an analog sensor, and it is available in different packages, as we can see in the [datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/TMP35_36_37.pdf), the one that I am using is the [TO-92](https://en.wikipedia.org/wiki/TO-92), which comes with 3 pins (PIN 1, +VS; PIN 2, VOUT; PIN 3, GND).

The sensor relation between output voltage (Vout) and temperature is linear, at 10 mV/°C scale factor, as we can see in [Figure 6. Output Voltage vs. Temperature of the datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/TMP35_36_37.pdf). On **Table 4. TMP35/TMP36/TMP37 Output Characteristics**, we also notice a 0.5V (500 mV) offset from the TMP36. So we can calculate the the temperature using the following formula:

$$
Temp = \frac{Vout - 500}{10}
$$

We can connect the sensor to the Arduino in 2 ways:

- Directly to the 5V Arduino power supply. This power supply may contain noise depending on what power supply we are using to power the Arduino.
- To the built-in 3.3V power supply. This supply goes through a voltage regulator, and is a cleaner signal. If our power supply to the Arduino contains noise, we can improve sensor reading and stability using the Arduino built-in 3.3V supply. Or any other external clean power supply.

This setup can be used with any other analog sensor.

![TMP36 connected to Arduino 5V schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0450%20-%20TMP36%20Temperature%20sensor/0450%20-%20TMP36%20Temperature%20sensor%205V.png?raw=true)

When using the 3.3V Arduino power supply we also need to connect the power supply to the [AREF (Analog Reference) pin](https://support.arduino.cc/hc/en-us/articles/360018922239-About-the-AREF-pin), to notify is that the max supply we are getting now is 3.3V.

![TMP36 connected to Arduino 3.3V schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0450%20-%20TMP36%20Temperature%20sensor/0450%20-%20TMP36%20Temperature%20sensor%203V3.png?raw=true)

### Using the TMP36 to measure temperature

We initial set the power supply in millivolts. When using a different power supply, from the standard built-in 5V, we need to configure the reference voltage used for analog input with [analogReference()](https://docs.arduino.cc/language-reference/en/functions/analog-io/analogReference/).

In the `loop` we get a reading and convert it to millivolts, then we convert the milivolts to temperature in celsius.

```c++
const int supplyMilliVolts = 3300; // Use 5000 for 5V standard power supply, or 3300 for 3.3V Arduino built-in power supply/

void setup() {
  analogReference(EXTERNAL); // Comment out if using the standard built-in 5V standard power supply.
  Serial.begin(9600);
}

void loop() {
  int reading = analogRead(A0);
  Serial.print(reading);
  Serial.println(" analog reading");

  float milliVolts = reading * (supplyMilliVolts / 1024.0);
  Serial.print(milliVolts);
  Serial.println(" mV");

  float temperatureC = (milliVolts - 500) / 10.0;
  Serial.print(temperatureC);
  Serial.println(" ºC");

  delay(2000);
}
```

## Measuring temperature with the MCP9808

The [MCP9808](https://www.microchip.com/en-us/product/mcp9808) is an high accuracy temperature sensor (±0.5°C). It communicates through the I²C protocol, and it has a customizable I²C address. [Microchip MCP9808 Datasheet](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ProductDocuments/DataSheets/MCP9808-0.5C-Maximum-Accuracy-Digital-Temperature-Sensor-Data-Sheet-DS20005095B.pdf). The sensor is available in different packages:

- [Adafruit MCP9808 High Accuracy I²C Temperature Sensor Breakout - STEMMA QT / Qwiic](https://www.adafruit.com/product/5027)
- [Adafruit MCP9808 High Accuracy I²C Temperature Sensor Breakout Board](https://www.adafruit.com/product/1782)
- [Seeed Studio Grove - I²C High Accuracy Temperature Sensor(MCP9808)](https://wiki.seeedstudio.com/Grove-I2C_High_Accuracy_Temperature_Sensor-MCP9808/)

![MCP9808 Arduino connection schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0460%20-%20Temperature%20with%20the%20MCP9808/0460%20-%20Temperature%20MCP9808.png?raw=true "MCP9808 Arduino connection schematics")

## Measuring atmospheric pressure with BMP180

The BMP180 is a digital sensor from Bosch, that we can use to [measure atmospheric pressure](https://en.wikipedia.org/wiki/Pressure_measurement) and temperature, the sensor communicates through I²C. at the moment this sensor is outdated and [Bosch as released new versions](https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/).

[BMP180 Digital pressure sensor datasheet](https://cdn-shop.adafruit.com/datasheets/BST-BMP180-DS000-09.pdf).

- [Adafruit BMP180 Barometric Pressure/Temperature/Altitude Sensor- 5V ready](https://www.adafruit.com/product/1603)
- [Seeed Studio Grove - Barometer Sensor (BMP180)](https://wiki.seeedstudio.com/Grove-Barometer_Sensor-BMP180/)

![BMP180 Arduino connection schematics](https://github.com/futureshocked/ArduinoSbSGettingStarted/blob/master/Schematics/0480%20-%20BMP180%20environment%20sensor/0480%20-%20BMP180%20environment%20sensor.png?raw=true "BMP180 Arduino connection schematics")

NEED SENSOR TO TEST
