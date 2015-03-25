We have driven a button input into our Pi. Now let’s control a LED output from our Pi. Make the following additions to your breadboard (after you have powered down your Pi!!).

![Breadboard](img/breadboard-5.png)

> Make sure to connect the short end of the LED to the 220 ohm resistor and the long end of the LED to pin 4 of the Pi.

The Python script that we will use for this circuit will turn the LED on and off when a button is pressed. Once your circuit is built, power your Pi back on, ssh into it, and cd into the piot directory. The Python script we will use is called `button-led.py`.

```
$ cd piot
$ nano button-led.py
```

**button-led.py**

```python
# Import library that lets you control the Pi's GPIO pins
import RPi.GPIO as io 
# Import time for delays 
from time import sleep

# Disables messages about GPIO pins already being in use
io.setwarnings(False)
# Numbering scheme that corresponds to breakout board and pin layout
io.setmode(io.BCM)

led_io_pin = 4
button_io_pin = 23
# Specifies that led_pin will be an output
io.setup(led_pin, io.OUT)
# Specifies that button_io_pin will be an input
io.setup(button_io_pin, io.IN)

button_on = False
previous_button_input = 0

while True:
    # Get the state of the button input
    button_input = io.input(button_io_pin)
    # Debounce the button
    if ((not prev_input) and button_input):
        # Toggle the button on and off
        button_on = not button_on
    prev_input = button_input
    sleep(0.05)
    
    if button_on:
        # Turn the LED on
        io.output(led_pin, io.HIGH)
    else:
        # Turn the LED off
        io.output(led_pin, io.LOW)
```

On line 4, we used a new library called time. This allows us to use the sleep command on line 29 (part of the button debounce logic). We specified the LED pin number as 4 on line 11 and set that pin to be an output on line 14. Instead of just reading if the button is on or off, line 27 toggles a variable, `button_on`, every time a button is pressed. Lines 31-36 either turn on or turn off the LED based on the state of `button_on`.

Run this script and press the button to see if the LED turns on and off.

```
$ sudo python button-led.py
```

[<< Part 3: Reading the Button](Part-3.-Reading-the-Button) - [Part 4: IoT Temperature Sensor >>](Part-4.-IoT-Temperature-Sensor)