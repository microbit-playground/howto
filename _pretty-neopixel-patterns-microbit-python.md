---
title: "Potentiometer and the Microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "How to create pretty, colourful patterns on the microbit in python with neopixels. How to use hue and not just RGB colour space."

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "Pretty patterns with neopixels on python."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: component examples

# Name of Component for index page
simple-description: Neopixel Examples

date: 2016-12-23T10:20:00Z
---

Examples of some pretty neopixel paterns on the microbit in Python.

[See the component article on this website about Neopixels.](/components/neopixels)

{:.ui .header .dividing}
### Shifting Rainbow
Create a list of values that range in hue. Every 100 milliseconds, shift the list by 1 and update the neopixel display.

<div class="ui top attached tabular menu" >
  <a class="item active" data-tab="first">Python</a>
  <a class="item" data-tab="second">PXT.io</a>
</div>
<div class="ui bottom attached tab segment active" data-tab="first" markdown="1">

{% highlight python %}
from microbit import *
import neopixel

def shift_left(lst, n):
    """Shifts the lst over by n indices

    >>> lst = [1, 2, 3, 4, 5]
    >>> shift_left(lst, 2)
    >>> lst
    [3, 4, 5, 1, 2]
    """
    assert (n > 0), "n should be non-negative integer"
    def shift(ntimes):
        if ntimes == 0:
            return
        else:
            temp = lst[0]
            for index in range(len(lst) - 1):
                lst[index] = lst[index + 1]         
            lst[index + 1] = temp
            return shift(ntimes-1)
    return shift(n)

def HSV_2_RGB(HSV):
    ''' Converts an integer HSV tuple (value range from 0 to 255)
    to an RGB tuple '''

    # Unpack the HSV tuple for readability
    H, S, V = HSV

    # Check if the color is Grayscale
    if S == 0:
        R = V
        G = V
        B = V
        return (R, G, B)

    # Make hue 0-5
    region = H // 43;

    # Find remainder part, make it from 0-255
    remainder = (H - (region * 43)) * 6;

    # Calculate temp vars, doing integer multiplication
    P = (V * (255 - S)) >> 8;
    Q = (V * (255 - ((S * remainder) >> 8))) >> 8;
    T = (V * (255 - ((S * (255 - remainder)) >> 8))) >> 8;

    # Assign temp vars based on color cone region
    if region == 0:
        R = V
        G = T
        B = P

    elif region == 1:
        R = Q;
        G = V;
        B = P;

    elif region == 2:
        R = P;
        G = V;
        B = T;

    elif region == 3:
        R = P;
        G = Q;
        B = V;

    elif region == 4:
        R = T;
        G = P;
        B = V;

    else:
        R = V;
        G = P;
        B = Q;

    return (R, G, B)


# 24 neopixels on pin0
np = neopixel.NeoPixel(pin0, 24)

# each neopixel shifts in value by 24
hue_step = round(255 / len(np))

# populate neopixel list with colours
for pixel in range(0, len(np)):
    hue = pixel * hue_step
    hsv = HSV_2_RGB((hue, 255,255))
    np[pixel] = hsv
    print(np[pixel])

while True:
    shift_left(np, 1)
    np.show()
    sleep(100)
{% endhighlight %}

* [Idea from PXT](https://github.com/Microsoft/pxt-neopixel)
* `shift_left()` function from [StackExchange](http://codereview.stackexchange.com/questions/88684/shift-elements-left-by-n-indices-in-a-list)
* `HSV_2_RGB()` function from Literate Programs


</div>

<div class="ui bottom attached tab segment" data-tab="second">
Much nicer in PXT!

{% highlight javascript %}
let neopixels = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
neopixels.showRainbow(1, 360)
basic.forever(() => {
    neopixels.rotate(1) // shift array
    neopixels.show()
    basic.pause(100)
})
{% endhighlight %}
</div>
