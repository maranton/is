Once everything is wired up (you should be getting pretty good at this by now), power up your Pi. The python script we will be using is inside the piot directory and is called sensors.py.

```
$ cd piot
$ ls
```

You should see sensors.py listed. 

> **Note** If you do not see sensors.py listed because you started this tutorial prior to Aug 19, 2015 (when it was created), you can find this file at https://github.com/InitialState/piot-101/blob/master/sensors.py (simply copy and paste it into a new file). Alternatively, you can re-clone your piot directory:
```
$ cd ~
$ git clone https://github.com/InitialState/piot-101.git piot
```

sensors.py
```python
import os
import glob
import time
import RPi.GPIO as io
import thread
from ISStreamer.Streamer import Streamer

# --------- User Settings ---------
BUCKET_NAME = ":computer: Sensors"
BUCKET_KEY = "piot_sensor_stream082315"
ACCESS_KEY = "PUT_YOUR_ACCESS_KEY_HERE"
TEMPERATURE_TOO_HIGH_F = 85
TEMPERATURE_TOO_LOW_F = 50
# ---------------------------------

io.setmode(io.BCM)
door_pin = 23
io.setup(door_pin, io.IN, pull_up_down=io.PUD_UP)

os.system('modprobe w1-gpio')
os.system('modprobe w1-therm')

base_dir = '/sys/bus/w1/devices/'
device_folder = glob.glob(base_dir + '28*')[0]
device_file = device_folder + '/w1_slave'

def read_temp_raw():
    f = open(device_file, 'r')
    lines = f.readlines()
    f.close()
    return lines


def read_temp():
    lines = read_temp_raw()
    while lines[0].strip()[-3:] != 'YES':
        time.sleep(0.2)
        lines = read_temp_raw()
    equals_pos = lines[1].find('t=')
    if equals_pos != -1:
        temp_string = lines[1][equals_pos+2:]
        temp_c = float(temp_string) / 1000.0
        return temp_c

def stream_temp(streamer):
    while True:
        temp_c = read_temp()
        temp_f = temp_c * 9.0 / 5.0 + 32.0
        if temp_f > TEMPERATURE_TOO_HIGH_F:
            streamer.log("Status", ":fire:")
        elif temp_f < TEMPERATURE_TOO_LOW_F:
            streamer.log("Status", ":snowflake:")
        else:
            streamer.log("Status", ":thumbsup:")
        streamer.log("temperature (C)", temp_c)
        streamer.log("temperature (F)", temp_f)
        print "Temperature: " + str(temp_f) + " F"
        streamer.flush()
        time.sleep(.5)

def main():
    streamer = Streamer(bucket_name=BUCKET_NAME, bucket_key=BUCKET_KEY, access_key=ACCESS_KEY)
    # Start temperature stream thread
    try:
       thread.start_new_thread(stream_temp, (streamer, ))
    except:
       print "Error: unable to start temperature streamer thread"

    # Door sensor
    door_status = 1
    while True:
        ## if the switch is open
        if (io.input(door_pin) == True and door_status != 0):
            streamer.log(":door: Door", "Open") 
            print "Door Open"
            streamer.flush() 
            door_status = 0 
        ## if the switch is closed 
        if (io.input(door_pin) == False and door_status != 1):
            streamer.log(":door: Door", "Close") 
            print "Door Closed"
            streamer.flush() 
            door_status = 1 
        time.sleep(2)

if __name__ == "__main__":
    main()            
```

Edit this file and place your access key in line 11 where it says "PUT_YOUR_ACCESS_KEY_HERE" (otherwise, you won't be streaming any sensor data into your account, and the rest of this section won't be very fun). You only have to modify line 11 as it assigns your access key to a global variable that is used in the Streamer constructor on line 62.

Run the script

```
$ sudo python sensors.py
```

This script streams the data from both sensors to Initial State and outputs the sensor values to the prompt. The prompt output will help you troubleshoot any issues you might have with wiring your circuit. You should see something similar to the following:

```
Temperature: 63.5 F
Temperature: 58.6616 F
Temperature: 55.0616 F
Temperature: 52.25 F
Door Open
Temperature: 50.1116 F
Temperature: 48.425 F
Temperature: 46.9616 F
Temperature: 45.8366 F
Temperature: 44.825 F
Temperature: 43.925 F
```

**Bonus Information to up your nerd cred:** Since we are collecting data from two sensors inside of one script, we had to do something a little special in the sensors.py code. The temperature sensor needs to report temperature on a regular interval (like a heartbeat). The door sensor needs to report open/closed when the event happens. Combining these two operations in sequence would be awkward (e.g. if we put the script to sleep for 10 seconds between temperature reads and a door sensor event happens when we are asleep, then the event is missed). To make this a bit cleaner, the temperature streaming code was launched as a "thread" on line 65 (thread.start_new_thread(stream_temp, (streamer, ))). The code inside of a thread executes, essentially, independently of the code outside of that particular thread. This allows the temperature streaming code to run on an interval (using the time.sleep(#) command to insert a controlled delay) without ever missing a door sensor event. You still have to be careful that you aren't blasting the processor with stuff to do in one thread (or outside of all threads) where it has no opportunity to execute the code in other threads. Doing this could peg the CPU at 100% usage. This is why there is a time.sleep(2) on line 84.

[<< Part 6: Hardware Setup](Part-6.-Hardware-Setup) - [Part 6: Building Your Dashboard >>](Part-6.-Building-Your-Dashboard)