---
title: "Add Python Modules to the Microbit"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Add Python modules containing statements, functions and classes to the microbit in the mu editor"

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "Add Python modules to the the microbit with mu editor."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: python

# Name of Component for index page
simple-description: Add Python Modules to the microbit

date:         2016-12-23T10:20:00Z
date-updated: 2016-12-23T10:20:00Z
---

{{ page.collection }}
### Introduction to Modules

Modules are a handy way of moving objects, such as functions and classes, out of your main script.

Each Python script on the microbit begins with the line:

```
from microbit import *
```

This imports everything (*) in the microbit module into the program.

We could only import certain objects from the microbit module:

```
from microbit import display
```

Importing the display module reveals the `display` functions. `display.scroll("hello")` would work but not `sleep(20)` because the `sleep` function was not imported.

Sometimes, when memory becomes tight, it is necessary to import only what your program needs.

### Adding 3rd Party Modules

To control a servo we need to import a module to tell the microbit how to use it.

In this example, we'll use [this servo class on github.](https://raw.githubusercontent.com/microbit-playground/microbit-servo-class/master/servo.py)

Download the file but _we cannot just copy the file to the microbit;_ it must be added to the Python filesystem within mu.

#### Upload the Module

To add a servo.py file click 'files' within mu. It lists the files on your computer and the files on the microbit.

Copy the servo.py file from your computer to the microbit by double-clicking it.

The `servo.py` file should be in the `mu` directory on your computer. On windows this is `c:\users\username\mu_code`.

#### Import the Module in your Script

In your python script you can import the `Servo` class from the servo.py file:

```
from microbit import *

from servo import Servo
# from servo.py import Servo class
```

#### Use the Module

```
Servo(pin0).write_angle(90)
```

Here the `Servo` class is called with the `pin0` argument. It tells an instance of the class that the servo's `SIGNAL` pin is connected to `pin0`.

It then calls the `.write_angle` function with the argument `90` to move the servo 90 degrees.

{% include box.html content="mu-where-is-upload-folder" %}

### Notes

* This will require two flashes within mu: the first flash is the program and will trigger an error since it cannot find the servo.py file. The second flash uploads the servo.py file.
