# KXTJ3-1057 Motion detection

Minified version of library for motion detection using low cost KXTJ3-1057, 3-axis MEMS accelerometer, low-power, ±2g/±4g/±8g/±16g full scale, high-speed I2C digital output, delivered in a 2x2x0.9mm LGAplastic package operating from a 1.71V–3.6V DC supply. Working on an attiny402

[![License: GPL v3](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/jasdoge/KXTJ3-Min/blob/master/LICENSE)
[![GitHub last commit](https://img.shields.io/github/last-commit/jasdoge/KXTJ3-Min.svg?style=social)](https://github.com/jasdoge/KXTJ3-Min)

###  Current consumption of operating modes μA

Operating mode (HZ) | Low Power | High Resolution
----------------|-------------------|-----------
0.781|1.543|
1.563|1.635|
3.125|1.922|
6.25|2.488|
12.5|3.431|
25|5.784|
50|9.821|
100|18.15|
200|34.72|
400||156
800||156
1600||156

## Interrupt Threshold

Interrupt threshold sensitivity is compared to the top 12bits of the accelerometer 8g output value regardless of the resolution chosen:

> This value can be anything from 1 to 4095

* i.e 0.0039 (1/256) to 16 g (4095/256)

## Interrupt Duration

Interrupt event duration to trigger the interrupt pin is a function of events and Sample Rate:

> This value can be anything from 1 to 255

* i.e 5 event_counts / 6.25 Hz = 0.8 seconds

## Non-Activity Duration

Interrupt non-activity duration to *reset* the interrupt pin is a function of events and Sample Rate:

> This value can be anything from 1 to 255

* i.e 5 event_counts / 6.25 Hz = 0.8 seconds

## Known Limitations

* Only 8 and 12 bits modes are implemented (14-bit is not);
* Only non-latched interrupt is implemented;

## Credits

Github Shields and Badges created with [Shields.io](https://github.com/badges/shields/)




# Usage

The library runs off of a single header file, which saves memory. This however means you can only have one accelerometer per project. But that should be within the scope of this library as I want it to run on small and cheap microcontrollers.

The header file adds the ```Accelerometer``` namespace. You call that directly.

| Func | Args | Description |
| --- | --- | --- |
| bool begin | uint8_t accelRange = Accelerometer::RANGE_8G, uint8_t sampleRate = Accelerometer::SAMPLE_RATE_100H | Detect and configure the accelerometer |
| bool setInterrupt | uint16_t threshold, uint8_t moveDur, uint8_t naDur, bool polarity = HIGH | Sets up interrupt signal outputs |
| bool toggleStandby | bool enable = true | Sets the accelerometer into standby mode |


### Error handling

To add error handling, you can set Accelerometer::onError to a function with one uint8_t:
<pre>
void onError( uint8_t error ){
	Serial.printf("Got error: %i\n", error);
}
void setup(){
	Accelerometer::onError = &onError;
}
</pre>




