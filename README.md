| Supported Targets | ESP32-C6 |
| ----------------- | -------- |

# I2C connected MCP9808 temperature sensor

Code originally based on the "I2C Simple Example" (i2c_simple) and using the esp32-c6 as the default microprocessor.

`Note:` The structure of the directories and files have been moved around to better encapsulate a "driver" project similar to the ones used by Espressif on their [component registry](https://components.espressif.com/). To compile this code you must be within the "test_apps/" directory as this is the main project resides.

`Warning:` This project includes my version of the ".vscode" directory. You will need to delete this and replace it with the esp-idf auto generated version for your system. The project also includes an ".editorconfig" file containing formatting instructions. This can either be retained or replaced with your own version.

## Overview

The idea behind this code is to be able to write and read information from the MCP9808 sensor using the I2C serial interface. In addition the code for the MCP9808 is separated out as a kind of "driver module". This may end up being a futile endeavour as its my first esp idf project; we shall see!

## How to use this code

### Hardware Required

To run this code, you should have an ESP32-C6<sup>(1)</sup> device connected to an MCP9808 sensor. The MCP9808 sensor is a high accuracy temperature sensor by Microchip. The sensor can be found on breakout boards from various suppliers and the [product brief and datasheet](https://www.microchip.com/en-us/product/mcp9808) are available.

#### Configuration parameters:

The following values have defaults that can be altered in the `menuconfig`:

| I2C-MCP9808                           |
| ------------------------------------- |
| I2C_MASTER_SDA<sup>(2)</sup>          |
| I2C_MASTER_SCL<sup>(2)</sup>          |
| MP9808_SENSOR_ADDRESS<sup>(3)</sup>   |
| MCP9808_SENSOR_INTERRUPT_GPIO         |

For the default values see the `I2C-MCP9808` group within `menuconfig`.

### Build and Flash

`Note:` It is assumed you have set up and initialised the esp idf environment.

Enter:

`cd [where you cloned the repository]/test_apps/`

`idf.py set-target esp32c6` (replace esp32c6 with esp32 device).

`idf.py -p PORT flash monitor` to build, flash and monitor the project (replace PORT with the usb port).

(To exit the serial monitor, type ``Ctrl-]``.)

See the [Getting Started Guide](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html) for full steps to configure and use ESP-IDF to build standard esp-idf projects. While not specifically for this project the steps should be very similar.

## Example Output

```bash
I (...)
I (...)
I (...)

```

## Troubleshooting

(I'll be lucky if this works for myself so...)

## Notes

<sup>(1)</sup> Only tested with ESP32-C6, may work unchanged with other devices.

<sup>(2)</sup> Most breakout boards have pullup resisters added. Internal (microprocessor) pullup resisters are not used. If internal pullup resisters are used they may not be sufficient to hold the line level, so as a preference external ones should be used on new designs.

<sup>(3)</sup> On breakout boards the `A0`, `A1`, `A2` address configuration pins can be either pulled up or pulled down, via a resistor, which then requires the pins to be linked to `vdd` or `gnd`, to change the default address, depending on the breakout board. There is no standard so the "default" address may change. This can cause hours of frustration if you substitute one manufacturers board for another. You have been warned!
