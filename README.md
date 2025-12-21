# STOPNU traffic light controller board

## Introduction

The StopNU board is an interface board design to be used with an Heltec V3 board, with purpose to provide a LoRa synchronized traffic light system.
The board has the ability to process inputs from: an Ambient light sensor, 3 button IO channels, a QWIIC interface.
The board can control LED strips via 5V LED control output lines, and using QWIIC peripherals.
IO is also exposed to the 'Expansion connector', which provides a way to breakout IO to future boards.

## Power

The board will be provided 5V power, stabilized outside of the board.
Because the current consumption is limited to 1A, the board it self cannot provide power to LED's controlled by the board.

Even though 3.3V and 5V pins are provided with the expansion header, the total power of these two power railes combined is limited at 3W.

## Pin-out

### Ambient light sensor

The ambient light sensor this circuit is designed for is the [TEPT4400](https://www.vishay.com/docs/81341/tept4400.pdf), where the sensor is connected between the collector and emitter pin.
The current allowed through the sensor results in a voltage that needs to be decoded by the ESP32 micro controller ADC input pin.

The emitter is is connected to ADC pin GPIO02

### LED control outputs

The LED control output pins are level shifted to 5V TTL, in order to work with the WS2812 addressable LED's or compatible.
The pins are output only as the level shifter only works one way.

| LED output | GPIO   |
| ---------- | ------ |
| 1          | GPIO04 |
| 2          | GPIO03 |

### Digital input lines

In order for external input devices to work with the board, 3 input lines have been provided, that are routed through an opto-coupler in order to be more noise resistant.
The IO pins are pulled up to 5V, and need to be pulled down by the input device in order for the board to register an input.

When the pin is pulled down the current through the IO input is 5 mA.

| Button # | GPIO   |
| -------- | ------ |
| 1        | GPIO07 |
| 2        | GPIO06 |
| 3        | GPIO07 |

### QWIIC connector

The QWIIC connector is there to connect external I2C (IIC) sensors and IO modules to the board, providing an extra method of expansion.
The port complies with the pin out and specs as provided by [QWIIC Sparkfun page](https://www.sparkfun.com/qwiic), QWIIC products sold are compatible with this board.

Again for the QWIIC bus 3.3V power supply counts, 3W budget shared with the other peripherals on the board.

| QWIIC pin | GPIO   |
| --------- | -----  |
| SDA       | GPIO34 |
| SCL       | GPIO33 |

### Expansion connector

The expansion connector exposes the Heltec V3 pins useable for IO.
The pins that are connected to the buffered outputs on the bottom of the board are also exposed on the header, but without the buffering.

Please be aware that some pins exposed on the header are used by the Heltec V3 internally, and should be used with care.

Here a list of the Heltec V3 board pins and where they connect to on the expansion header.

| pin | GPIO    | capable        | comments                        |
| --- | ------- | -------------- | ------------------------------- |
| 1   | GND     | Power          |                                 |
| 2   | GND     | Power          |                                 |
| 3   | GPIO41  |                |                                 |
| 4   | GPIO44  |                | Heltec V3 UAR_TX                |
| 5   | GPIO40  |                | Drives Heltec white LED         |
| 6   | GPIO43  |                | Heltec V3 UART_RX               |
| 7   | GPIO39  |                | Heltec V3 external power switch |
| 8   | MCU_RST |                | Heltec V3 Reset pin             |
| 9   | GPIO38  |                | Heltec V3 ADC ctrl              |
| 10  | GPIO00  |                | USER_KEY                        |
| 11  | GPIO01  | ADC            |                                 |
| 12  | GPIO35  |                |                                 |
| 13  | GPIO02  | ADC            |                                 |
| 14  | GPIO34  |                | QWIIC SDA                       |
| 15  | +3.3V   | Power          | 3W max (total)                  |
| 16  | +5V     | Power          | 3W max (total)                  |
| 17  | GND     | Power          |                                 |
| 18  | GND     | Power          |                                 |
| 19  | GPIO03  | ADC            | LED channel 2                   |
| 20  | GPIO45  |                |                                 |
| 21  | GPIO04  | ADC            | LED channel 1                   |
| 22  | GPIO33  |                | QWIIC SCL                       |
| 23  | GPIO05  | ADC            | Button IN 3                     |
| 24  | GPIO46  |                |                                 |
| 25  | GPIO06  | ADC/Input only | Button IN 2                     |
| 26  | GPIO42  |                |
| 27  | GPIO07  | ADC/Input only | Button IN 1                     |
| 28  | GPIO26  |                |                                 |
| 29  | GND     | Power          |                                 |
| 30  | GND     | Power          |                                 |
