---
title: "Read Python Microbit Output Wirelessly"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Connect wirelessly to the microbit to read data over serial."

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "Use two microbits to read data over serial."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: communication

# Name of Component for index page
simple-description: Serial over Radio (Python)
---

Bluetooth is not available in Python for the microbit due to memory constraints. However, it is still possible to read (and write) data to the microbit wirelessly. 

To do this you will need to use the `radio` module and two microbits.

* TX Microbit: Wirelessly sends data to RX microbit.
* RX Microbit: Connected to the computer over USB. Receives data from TX microbit and outputs it to the serial.

{:.ui .dividing .header}
### Transmitting Microbit

Transmit `field_strength` from the compass to the second microbit.

{% highlight python %}

# TX microbit

import radio

from microbit import *

radio.on()

while True:
    field_strength = str(compass.get_field_strength())
    radio.send(field_strength)
    sleep(100)

{% endhighlight %}

{:.ui .dividing .header}
### Receiving Microbit

Receive data from the first microbit. `print()` can be read by connecting over serial to the microbit.

{% highlight python %}

# RX microbit

import radio

from microbit import *

radio.on()

while True:
    radio.receive():
      print(str(radio.receive()))
      sleep(100)
{% endhighlight %}

This code is effectively a metal detector; it can be changed with ease.