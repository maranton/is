SSH into your Pi and cd into the piot directory. There is a python script in this directory called button.py. This is the script we will use to read the button input. Let’s take a look at this script.

```
$ cd piot
$ nano button.py
```

**button.py**

```python
#Import library that lets you control the Pi's GPIO pinsimport RPi.GPIO as GPIO# Disable messages about GPIO pins already being in useGPIO.setwarnings(False)# Numbering scheme that corresponds to breakout board and pin layout 
GPIO.setmode(GPIO.BCM)pinNumBTN = 23GPIO.setup(pinNumBTN,GPIO.IN) # Specify that pinNumBTN will be an input prevInput = 0while True:    # Get the state of the button input
    btnInput = GPIO.input(pinNumBTN)
    if (btnInput != prevInput):        # When the button changes state, print its value        print btnInput
        prevInput = btnInput
```

The lines that begin with ‘#’ are comment lines, a great way to document code. This script imports a special library, RPi.GPIO, that allows you to read and write the Pi’s I/O pins. We set the input button to pin 23 on line 9, which matches our breadboard circuit. Pin 23 is set to an input pin on line 10. The “while loop” on line 13 will run until you kill the script and read the state of pin 23 and print its value only when it changes.

Using indentation in Python is not just a way to make your code more readable but is actually a part of Python syntax. Every line of code that is has at least one tab after the while True: statement is part of that while loop. Notice lines 17-19 have an additional tab indentation. This makes these lines a part of the if statement on line 16 (as well as part of the while loop).

We are ready to test our code. Run the following command:

```
$ sudo python button.py
```

We have to use the sudo prefix because accessing the Pi’s I/O requires super user access.

Pressing the button over and over should result in a 1 and a 0 being printed to the screen each time.

```
1
0
1
0
1
0
```

To stop the script, press `CTRL`+`c`.

[<< Step 3: Input Button](Step-3.-Input-Button) - [Step 3: Adding an LED >>](Step-3.-Adding-an-LED)