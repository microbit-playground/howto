---
title: "Potentiometer and the Microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Examples of using the potentiometer and the microbit."

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "Examples of using a Potentiometer with the microbit."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: component examples

# Name of Component for index page
simple-description: Potentiometer Examples

date: 2016-12-23T10:20:00Z
---

All examples use a simple 10k potentiometer.

[See the component article on this website about the LED.](/components/potentiometer)

{:.ui .header .dividing}
### Dimming LED
Dim and LED based on the reading/rotation of the potentiometer.
### Pot always pin 1

#### Hardware Required
* LED
* 220Ω resistor
* 10kΩ potentiometer

{:.ui .image}
![diagram for blinking LED](images/potentiometer-example-microbit-diagram.png)

<div class="ui top attached tabular menu">
<a class="item active" data-tab="first">Python</a>
<a class="item" data-tab="second">PXT.io</a>
</div>
<div class="ui bottom attached tab segment active" data-tab="first" markdown="1">
{% highlight python %}
from microbit import *

pot = pin1
led = pin0

while True:
    led.write_analog(pot.read_analog())
    sleep(100)
{% endhighlight %}

This should work a lot better than it does.

The LED flickers each time `write_analog()` is called. Hopefully someone has a solution.

</div>
<div class="ui bottom attached tab segment" data-tab="second" markdown="1">

{% highlight javascript %}
let potReading = 0

basic.forever(() => {
    potReading = pins.analogReadPin(AnalogPin.P1)
    pins.analogWritePin(AnalogPin.P0, potReading)
})

{% endhighlight %}

</div>



{:.ui .header .dividing}
### RGB Colour Mixing
Mix colours based on the reading from three potentiometers.

#### Hardware Required
* RGB LED
* 3 &times; 220Ω resistors
* 3 &times; 10kΩ potentiometer
* microbit breakout board

{:.ui .image}
![colour mixing diagram circuit](images/potentiometer-example-microbit-colour-mixing.png)

{% highlight python %}
from microbit import *

# potentiometer pins
red_pot = pin0
green_pot = pin1
blue_pot = pin2

# led pins
red_led = pin10
green_led = pin3
blue_led = pin4

while True:
    # get colors from pots
    # returned values range from 0 - 1023
    red = red_pot.analog_read()
    green = green_pot.analog_read()
    blue = blue_pot.analog_read()

    # write colours to LEDs
    red_led.analog_write(red)
    green_led.analog_write(green)
    red_led.analog_write(blue)

    sleep(100)
{% endhighlight %}
