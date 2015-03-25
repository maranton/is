With this circuit wired up and connected, power on your Pi. We’ve already installed the RPi.GPIO library and ISStreamer, and, unlike the temperature sensor, this door sensor doesn’t need any initialization. It basically acts like a button.

In order to make sure it’s working, we’re going to add some extra statements to our final script that print to the terminal like in our “Hello World”. Go to the piot directory and use nano to edit the script door.py.

```
$ nano door.py
```

**door.py**

```python
import time # so we can use "sleep" to wait between actions
import RPi.GPIO as io # import the GPIO library we just installed but call it "io"
from ISStreamer.Streamer import Streamer # import the ISStreamer

## name the bucket and individual access_key
#streamer = Streamer(bucket_name="Locker Protector", bucket_key="locker_protector", access_key="YOUR_ACCESS_KEY_HERE")

is.setmode(io.BCM) # set GPIO mode to BCM
door_pin = 23 # enter the number of whatever GPIO pin your're using
io.setup(door_pin, io.IN, pull_up_down=io.PUD_UP) # use the built-in pull-up resistor

door=0 # initialize door

## Event loop
while True:
    ## if the switch is open
    if io.input(door_pin):
        #streamer.log("Door", "Open") # stream a message saying "Open"
        #streamer.flush() # send the message immediately
        door = 0 # set door to its initial value
        time.sleep(1) # wait 1 second before the next action
    ## if the switch is closed and door does not equal 1
    if (io.input(door_pin) == False and door != 1):
        #streamer.log("Door", "Close") # stream a message saying "Close"
        #streamer.flush() # send the message immediately
        door = 1 # set door so that this loop won't act again until the switch has been opened
```

You’ll notice that the streamer statements are commented out with a `#`. This is because we want to test the switch before streaming anything.

Underneath each respective `streamer.flush()` statement, we are going to add:

```python
        print "Open"
```

```python
        print "Close"
```

Save the script and run it.

```
$ sudo python door.py
```

If the switch and magnet are sufficiently far apart, then you should see “Open” start printing down the screen. Bring the two together (less than an inch apart) and you should see “Close” print once. Move them apart and “Open” will print again. Now we’re in business!


[<< Part 5: Hardware Setup](Part-5.-Hardware-Setup) - [Part 5: A Live Security Data Stream](Part-5.-A-Live-Security-Data-Stream)