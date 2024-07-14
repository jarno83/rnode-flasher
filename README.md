# RNode Flasher

A web based firmware flasher for [Reticulum](https://github.com/markqvist/Reticulum) / [RNode_Firmware](https://github.com/markqvist/RNode_Firmware).

- It is written in javascript and uses the [Web Serial APIs](https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API).
- It supports putting a device into DFU mode.
- It supports flashing `application` firmware from a zip file.

At this time, it does not support flashing bootloaders or softdevices.

## How does it work?

I wanted something simple, for flashing RNode firmware to a nRF52 RAK4631 in a web browser.

So, I spent a bit of time working through the source code of [adafruit-nrfutil](https://github.com/adafruit/Adafruit_nRF52_nrfutil) and wrote a javascript implementation of [dfu_transport_serial.py](https://github.com/adafruit/Adafruit_nRF52_nrfutil/blob/master/nordicsemi/dfu/dfu_transport_serial.py)

Generally, you would use the following command to flash a firmware.zip to your device;

```
adafruit-nrfutil dfu serial --package firmware.zip -p /dev/cu.usbmodem14401 -b 115200 -t 1200
```

The [nrf52_dfu_flasher.js](./nrf52_dfu_flasher.js) in this project implements a javascript, web based version of the above command.

There was an existing package called [pc-nrf-dfu-js](https://github.com/NordicSemiconductor/pc-nrf-dfu-js), however this repo had been archived and didn't appear to support the latest DFU protocol.

## How to use it?

- Open [index.html](./index.html) in your web browser.
- Put your device into DFU mode.
- Select a firmware file and click flash.
- Your device should reboot into the new firmware.

> Note: At this time, firmware hashes for RNode are not configured. This is next on the todo list.

## Device Support

The following list of devices are supported:

- RAK4631

## TODO

- support configuring eeprom with device signatures and firmware hashes
- support configuring tnc mode, also useful for the [transport node firmware](https://github.com/attermann/microReticulum_Firmware/commits/transport_node/)
- support other devices, such as ESP32/Heltec V3
- support flashing existing firmware files from api

## License

MIT

## References

- https://github.com/adafruit/Adafruit_nRF52_nrfutil
- https://github.com/adafruit/Adafruit_nRF52_nrfutil/blob/master/nordicsemi/dfu/dfu_transport_serial.py
- https://github.com/markqvist/RNode_Firmware/blob/master/RNode_Firmware.ino
- https://github.com/markqvist/RNode_Firmware/blob/master/Framing.h
- https://github.com/markqvist/RNode_Firmware/blob/master/Utilities.h
