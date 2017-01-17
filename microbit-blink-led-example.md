---
title: "Blink an LED with Microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Classic example of blinking an LED on the microbit."

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "How to Blink an LED on the Microbit."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: component examples

# Name of Component for index page
simple-description: Blink LED

video:
  teaser: microbit_blink_led_example

date: 2016-12-23T10:20:00Z
---

The classic example of a simple blinking LED

[See the component article on this website about the LED.](/components/single-led)

{:.ui .header .dividing}
### Blinking LED

#### Hardware Required
* LED
* 220Ω resistor

{:.ui .image}
![diagram for blinking LED](images/microbit-blink-led-example-diagram.png)

{% highlight python %}
from microbit import *

while True:
    pin0.write_digital(1)  # on
    sleep(100)
    pin0.write_digital(0)  # off
    sleep(100)
{% endhighlight %}
