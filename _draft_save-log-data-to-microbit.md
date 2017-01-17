---
title: "Logging Data to the Microbit with Python"
layout: text-width-sidebar

# Meta description for google and sharing
meta-description:  "Log Data to the Microbit with python"

#############
## Options ##
#############

share: true
author: jez

#################################
## Component Template Specific ##
#################################

# About Box is on the left of the program page
about: "You can store a small amount of data from the microbit to the device with python."

# Category of howto: I2C, other, visual basic, component examples, python, data logging
cats: datalogging

# Name of Component for index page
simple-description: Save to Device

date: 2016-12-23T10:20:00Z
---

```
Draft Notes:

All data written to a file must be stored in memory before writing. This is around 8k.
The data could be split into multiple files and then written.

This is a scratchpad; everything that follows in wrong.

```
Python on the microbit has a small file system which can use to read and save files. It's also possible to list and delete files. It's persistent meaning anything saved there will persist during power cycles and resets. However, flashing a new program in mu will wipe the saved files.

There is around 30K of memory which is plenty for data logging.

Unfortunately the file cannot be appended to. This means you cannot add a new reading to the end of a file; a new file must be made each time you want to write.

### Opening a file

Python reads and writes to files using the `open` function. It is used in conjunction with a `with` statement:

{% highlight python %}
with open('textfile.txt', 'w') as my_file:
    my_file.write("Hello!")
    my_file.close()
display.scroll("I wrote to a file!")
{% endhighlight %}

The `with` statement uses the `open` function to open the file and assign it to an object. In the above example, `textfile.txt` is assigned to be the object `my_file`.

#### Open Mode
The `open` function has two arguments: the first---`textfile.txt`---tells Python the name of the file it wishes to use.

The second argument is __a__ which tells Python which mode to use to open the file. There are a few modes:

{:.ui  .basic .striped .table}
| r | Open a text file for reading |
| w | Create a text file for writing. If the file exists, overwrite it. |
| rb | Open a binary file for reading. |
| wb | Create a binary file for writing. If the file exists, overwrite it. |

### Writing to a file

#### `.write` method

Writing to a file is achieved through the `.write` method. It takes (and only takes) a string as the argument in `r` mode.

#### Line Ending Fun

This adds a carriage return (`\r`) and new line(`\n`) each time `Hello` is printed.

```
my_file.write("Hello!\r\nHello!\r\nHello!\r\n")
```

 If you download the `textfile.txt` file and look at it in notepad on Windows, it looks something like this:

```
Hello!
Hello!
Hello!

```

If using a Mac or Linux, only a `\n` is needed.


#### Outputting Comma Separated Values Data

We will output the data from the microbit into a CSV file so it can be imported into Excel.

CSV files are, as the name suggest, a list of values separated by a comma. At the end of each sequence of data points, we will add a new line character.

We want to get this from the microbit:

```
24,434
24,434
23,435
23,434
```

### Memory

There is 8k of memory and 32k on the file system if no modules are imported into the microbit.

Everything written to a file on the microbit must be held in memory first. Therefore, despite having 32k of RAM, we can only write around 8k to file.

The solution is to write data to multiple files:

1. Store log data in RAM as the variable `data2write`.
2. When RAM is full, write `data2write` to a __file1.txt__
3. Clear the `data2write` variable to free RAM.
4. Store log data in RAM as the variable `data2write`.
5. When RAM is full, write `data2write` to a __file2.txt__
6. Clear the `data2write` variable to free RAM.

This repeats until the microbit runs out of the 32k on its file system. This results in sequentially numbered files, each around 8k.

### Final Code

A few words about the final code:

#### `from microbit import gc, sleep`

Explicit imports are used to import `gc` and `sleep`. This saves RAM as we do not `display` or `i2c` and other functions.

More RAM results in fewer files.

#### `gc.collect()`

The imported `gc` module is for garbage collection. `gc.collect()` runs a garbage collection; no idea how this works but it frees memory.

#### `if button_a.is_pressed():`

The microbit begins logging if `button_a` is pressed. Without this line, the microbit begins logging immediately and overwrites files if it's reset (ie. you plug it into a computer to retrieve the logged data).

{% highlight python %}

from microbit import gc, sleep

minutes-between-logging = 5     # Set interval of logging

#############
# Functions #
#############

# write data2log to sequentially numbered file
def write2file():
    counter += 1
    filename = "log%s.csv" % counter       # log1.csv log2.csv ...
    with open(filename, 'w') as my_file:
        my_file.write(data2write)
        my_file.close()
    return

# Is the microbit's memory full?
def is_memory_full()
    if gc.mem_free() < 1000:   # if < 1 kb of ram
        return True
    return False

################
# Main Program #
################

counter = 0
data2write = ""


if button_a.is_pressed():
    while True:

        # Log variables to data2write
        running-time = str(counter * minutes-between-logging)
        temperature = str(temperature())
        data2write = data2write + temperature + "," + running-time + "\r\n"

        # sleep
        sleep(minutes-between-logging * 60000) # convert minutes to milliseconds

        # If RAM is full, save logged data to file
        if is_memory_full()
            write2file()
            data2write = ""    # Clear data2write variable
            gc.collect()       # Reclaim RAM
{% endhighlight %}

from microbit import sleep, button_a, temperature
import gc

data2write = ""
counter = 0
#############
# Functions #
#############

# write data2log to sequentially numbered file
def write2file():
    global counter
    counter += 1
    filename = "log%s.csv" % counter       # log1.csv log2.csv ...
    with open(filename, 'w') as my_file:
        my_file.write(data2write)
        my_file.close()
    print("Written file")
    return

# Is the microbit's memory full?
def is_memory_full():
    if gc.mem_free() < 1000:   # if < 1 kb of ram
        print("Memory is full")
        return True
    return False

################
# Main Program #
################

minutes_between_logging = 5     # Set interval of logging

print("press button_a \n")

while True:
    print("press a")
    if button_a.was_pressed():
        while True:
            print("logging...")
            # Log variables to data2write
            running_time = str(counter * minutes_between_logging)
            temp = str(temperature())
            data2write = data2write + temp + "," + running_time + "\r\n"

            print("running_time:" + str(running_time))
            print("temp:" + str(temp))
            print("memory:" + str(gc.mem_free()))


            # sleep
            sleep(minutes_between_logging * 60) # convert minutes to milliseconds

            # If RAM is full, save logged data to file
            if is_memory_full():
                write2file()
                data2write = ""    # Clear data2write variable
    sleep(100)



=============== with a list


from microbit import sleep, button_a, temperature
import gc

data2write_list = []
counter = 0
#############
# Functions #
#############

# write data2log to sequentially numbered file
def write2file():
    global counter
    counter += 1
    filename = "log%s.csv" % counter       # log1.csv log2.csv ...
    with open(filename, 'w') as my_file:
        my_file.write(str(data2write_list))
        my_file.close()
    print("Written file")
    return

# Is the microbit's memory full?
def is_memory_full():
    if gc.mem_free() < 1000:   # if < 1 kb of ram
        print("Memory is full")
        return True
    return False

################
# Main Program #
################

minutes_between_logging = 5     # Set interval of logging

print("press button_a \n")

while True:
    print("press a")
    if button_a.was_pressed():
        while True:
            print("logging...")
            # Log variables to data2write
            running_time = counter * minutes_between_logging
            data2write_list.append([running_time, temperature()])

            print("memory:" + str(gc.mem_free()))


            # sleep
            sleep(minutes_between_logging * 60) # convert minutes to milliseconds

            # If RAM is full, save logged data to file
            if is_memory_full():
                write2file()
                data2write_list = []    # Clear data2write variable
    sleep(100)


==== refreshed


from microbit import sleep, button_a, temperature
import gc

data2write = ""
counter = 0
#############
# Functions #
#############

# write data2log to sequentially numbered file
def write2file():
    global counter
    counter += 1
    filename = "log%s.csv" % counter       # log1.csv log2.csv ...
    with open(filename, 'w') as my_file:
        my_file.write(data2write)
        my_file.close()
    print("Written file")
    return

# Is the microbit's memory full?
def is_memory_full():
    if gc.mem_free() < 1500:   # if < 1 kb of ram
        print("Memory is full")
        return True
    return False

################
# Main Program #
################

minutes_between_logging = 5     # Set interval of logging

print("press button_a \n")

while True:
    print("press a")
    if button_a.was_pressed():
        while True:
            print("logging...")
            # Log variables to data2write
            running_time = str(counter * minutes_between_logging)
            temp = str(temperature())
            data2write = data2write + temp + "," + running_time + "\r\n"

            print("running_time:" + str(running_time))
            print("temp:" + str(temp))
            print("memory:" + str(gc.mem_free()))


            # sleep
            sleep(minutes_between_logging * 2) # convert minutes to milliseconds

            # If RAM is full, save logged data to file
            if is_memory_full():
                write2file()
                data2write = ""    # Clear data2write variable
    sleep(100)

----
final

from microbit import sleep, button_a, temperature

import gc

minutes_between_logging = 5     # Set interval of logging

running_time = 0
data2write = ""
counter = 0


def write2file():
    global counter
    counter += 1
    filename = "log%s.csv" % counter       # log1.csv log2.csv ...
    with open(filename, 'w') as my_file:
        my_file.write(data2write)
        my_file.close()
    print("Written: " + filename)
    return


def is_memory_full():
    if gc.mem_free() < 1500:   # if < 1 kb of ram
        return True
    return False


while True:
    if button_a.was_pressed():
        print("logging...")
        while True:
            # Log temperature() & running_time to data2write
            gc.collect()
            temp = str(temperature())
            data2write = data2write + str(temperature()) + "," + str(running_time) + "\r\n"

            sleep(minutes_between_logging)  # minutes to milliseconds
            running_time += minutes_between_logging

            if is_memory_full():
                write2file()
                data2write = ""
    sleep(100)

    --- fional

    from microbit import sleep, button_a, temperature
import gc

minutes_between_logging = 5     # Set interval of logging

running_time = 0
data2write = ""
counter = 0

def write2file():
    global counter
    counter += 1
    filename = "log%s.csv" % counter       # log1.csv log2.csv ...
    with open(filename, 'w') as my_file:
        my_file.write(data2write)
        my_file.close()
    print("written file: " + filename)
    return

def is_memory_full():
    if gc.mem_free() < 1500:   # if < 1.5k of ram
        return True
    return False

################
# Main Program #
################

print("press button_a to log")

while True:
    if button_a.was_pressed():
        print("logging...")
        while True:
            gc.collect()
            # Log variables to data2write
            data2write = data2write + str(temperature()) + "," + str(running_time) + "\r\n"

            # sleep between logs
            sleep(minutes_between_logging * 2) # convert minutes to milliseconds
            running_time += minutes_between_logging

            # If RAM is full, save logged data to file
            if is_memory_full():
                write2file()
                data2write = ""
    sleep(100)



Can anyone point me in the direction of a datalogger? Or give me a few pointers? I've been trying to write one but keep getting stuck


But I'm not getting a lot of storage on the microbit. It'll write 8 files of 1.5k each before I get OS error 8 (the device is full?). I thought there was 30k on the microbit as storage? Am I confused?


I add to the data2log variable each time a log is taken. When the memory of the microbit is full, I write the string variable in sequentially numbered files on the file system.
