# PDX Hackerspace 3D Printer Monitor

This is a simple device for monitoring 3D printers.

It hosts a [SeeedStudio Xiao ESP32S3 Sense](https://www.seeedstudio.com/XIAO-ESP32S3-Sense-p-5639.html) CPU camera module so that its users can see the status of their prints.

It also can use a BME280 or BME680 for environmental (air temperature and humidity) monitoring, as well as a PMS5003 for air quality/particulate matter.

It includes an optional connection to an I2C display or a larger SPI-based RGB display, and can drive an addressable RGB LED strip for lighting.

## Modifying the Xiao S3 Sense

The Xiao S3 Sense has optional D11 and D12 pins. We can use these pins
to provide PWM signals to control an optional air filter fan, and to
run optional RGB LEDs on the fan. These signals are run through the
level shifter to bring them to 5V values.

Because we've run out of pins we need to use D11 and D12. By default
they're connected to the Xiao camera board's I2S microphone. The board
needs to be modified as documented
[here](https://wiki.seeedstudio.com/xiao_esp32s3_pin_multiplexing/#step-1-cut-off-the-connection-between-j1-and-j2).
Note that this web page incorrectly states the GPIO numbers for D11
and D12. D11 is actually GPIO42 and D12 is actually GPIO41.

## PCB

The PCB is designed using KiCAD. Hardware revisions are stored in the hardware directory.

You can [order this PCB from OSHPark](https://oshpark.com/shared_projects/bLoBvODi) but please don't order it. This project is under active albeit slow development. There will be a better version available soon.

![PCB front](images/0.5.1-front.jpg) ![PCB back](images/0.5.2-back.jpg) 

## Software

The board is intended to integrate with Home Assistant. ESPHome is the easiest way to build code for it. The repo contains an example ESPHome definition file at esphome.yml, which needs its display functionality fleshed out.

## OV5640

https://github.com/0015/ESP32-OV5640-AF


## PrusaLink

Status observed:
- finished
- idle
- busy
- attention
- printing




