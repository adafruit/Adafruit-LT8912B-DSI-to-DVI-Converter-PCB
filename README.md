## Adafruit LT8912B DSI to DVI Converter PCB

<a href="http://www.adafruit.com/products/6539"><img src="assets/6539.jpg?raw=true" width="500px"><br/>
Click here to purchase one from the Adafruit shop</a>

PCB files for the Adafruit LT8912B DSI to DVI Converter. 

Format is EagleCAD schematic and board layout
* https://www.adafruit.com/product/6539

### Description

You've likely used I2C or SPI to connect to small displays on your microcontroller: these two protocols are great for small OLEDs and TFTs, maxing out at about 320x480 pixels. If you want to go bigger maybe you've stretched into TTL displays like on our ESP32-S3 Qualia which can go to 720x720, but TTL displays use a LOT of pins, like 30+ and they max out due to the limits of sloshing data over a parallel interface. So, the MIPI alliance came up with a high speed serial interface for displays...big surprise they call it DSI (display serial interface). We're starting to see more and more chips that come with DSI - this interface has been available on the Raspberry Pi computer series for a long time but now the [ESP32-P4](https://www.adafruit.com/product/6536) has it too. And more chips are coming out with DSI support as it becomes widely adopted.

If you have a chip or computer with DSI you can connect many panel displays to it, and now thanks to the <b>Adafruit LT8912B DSI to DVI Converter</b> you can connect a DSI output to a DVI or HDMI monitor! This converter chip will take that DSI signal and squish it around to the right format and connector that many TVs and monitors use, you can even use an HDMI capture dongle if you want to pipe the signal into a computer. It works with up to 4 lanes for 1080p60 max resolution.

One side has a 22-pin 0.5mm pitch FPC connector, this is the "Raspberry Pi 5" standard pinout (also used on compute-module boards) and we also use in on our [ESP32-P4 boards](https://www.adafruit.com/product/6536). [To connect to something with a similar 22-pin FPC connector](https://www.adafruit.com/product/6035), use this flex cable. If you have an older Raspberry Pi or some other DSI emitter with the 15-pin 1mm pitch connector, [use an adapter converter cable like this one](https://www.adafruit.com/product/5821). <b>Note we don't include a cable with this adapter because we dont know which one you need, so pick that up separately!</b>

Once the FPC is connected, you do have to configure the LT8912B over I2C. Thankfully there's an I2C lane on the FPC cable [so you can use our Arduino or CircuitPython drivers](https://github.com/adafruit/Adafruit_LT8912B) to set up the LT8912B for the resolution that matches the DSI output (and, ideally one that the DVI monitor supports!) On Raspberry Pi, [there's a kernel module](https://github.com/raspberrypi/linux/pull/7725) you can use - a device tree overlay will configure the chip resolution. [Espressif has their own ESPIDF driver](https://components.espressif.com/components/espressif/esp_lcd_lt8912b) as well. Note that this chip requires signing an NDA to get full datasheet and driver support so we've cobbled together our support using publicly available info, and it works just fine - but we won't be able to provide a full datasheet. (You're free to contact/sign with the chip maker if you like for in-depth support)

Astute folks may remember that DVI/HDMI monitors also have an I2C device built-in on 0x50 for EDID detection so you can determine supported resolutions and modes. We connect those I2C lines (called DDC) to the same I2C lines on the FPC so you can configure the LT8912B and also read the EDID at the same connection. This is great 99% of the time. But! If you happen to be connecting to an RTD266x-driven monitor, which is common for small maker-friendly displays, that controller also uses a conflicting I2C address to the LT8912B. So, basically, if you are connecting to an RTD266x-controlled-monitor, switch the DDC connection switch to 'off' and then you can read the DDC over the Stemma QT port or breakout pads at the top, make sure its on a second I2C port.

Finally, the most observant of all may see the I2S pins broken out and ask: hey can I also pipe I2S in to have that audio played on the monitor in question? The answer is: maybe? We broke out those pins and tried hard to get I2S audio working, but given we don't have the proper NDA'd datasheet there's no working example. We're pretty sure it can be done but I2S input is unsupported. If you figure it out let us know!

We've tested this a bunch on the [ESP32-P4](https://www.adafruit.com/product/6536) and Raspberry Pi 5 - it ought to work on other DSI sources but we've not tried it out ourselves. Despite using the same connector as the HSTX this is not going to work with the RP2350. Check that your source uses the same pinout as the Raspberry Pi 5 to make sure it will work!

### License

Adafruit invests time and resources providing this open source design, please support Adafruit and open-source hardware by purchasing products from [Adafruit](https://www.adafruit.com)!

Designed by Limor Fried/Ladyada for Adafruit Industries.

Creative Commons Attribution/Share-Alike, all text above must be included in any redistribution. 
See license.txt for additional details.
