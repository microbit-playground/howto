---
title: "Scan the I2C bus of the Microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Scan the microbit I2C bus for connected slave devices."

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "Scan the I2C bus for slave devices."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: I2C

# Name of Component for index page
simple-description: I2C Bus Scan

date:         2016-12-23T10:20:00Z
date-updated: 2016-12-23T10:20:00Z
---
I2C and SPI are protocols that can link the microbit to other devices, such as an LED matrix or an accelerometer.

There is more about connecting I2C devices to you microbit [in this _how to_ article.](/howto/attach-microbit-to-I2C-devices)

There are devices already on the I2c bus: the microbit's onboard accelerometer and magnetometer (or compass).

The I2C bus is exposed on the microbit's `pin19` & `pin20`. Additional devices can be attached to the bus with these pins.

Connecting components in this way results in fewer wires for communication: SPI uses three wires, I2C requires two.

As mentioned, there are already two devices connected to the microbit on the I2C bus:

{:.ui .basic .small .table}
| Device | I2C Address |
|--------|----------|
| Accelerometer | `0x1D` |
| Magnetometer (compass) | `0x0E` |

Each component added to `pin19` & `pin20` requires an address. Each device has an address 'hard coded' into the component. These are usually these are written in the datasheet of the I2C device. Often the address of the device can be changed with jumpers or soldering contact points.

### Scan the Bus

It is also possible to scan the I2C bus for the device if you cannot find it in the datasheet. This program will return a list of the connected devices when button_a is pressed. You'll need to be connected over serial to the microbit to read it.

It's based on micropython's `.scan` method.

{% highlight python %}
from microbit import *

start = 0x08
end = 0x77

while True:
    display.show(Image.ARROW_W)
    if button_a.was_pressed():
        display.show(Image.MEH)
        print("Scanning I2C bus...")
        for i in range(start, end + 1):
            try:
                i2c.read(i, 1)
            except OSError:
                pass
            else:
                print("Found:  [%s]" % hex(i))
        print("Scanning complete")
        print("Magnetometer [0x0e] Accelerometer [0x1d]")
    sleep(10)
    {% endhighlight %}
### See also
