With this circuit wired up and connected, power on your Pi. The latest version of Raspbian (kernel 3.18) requires an addition to your /boot/config.txt file for the Pi to communicate with the DS18B20. Run the following to edit this file:

```
$ sudo nano /boot/config.txt
```

If the following line is not already in this file (if it is, it is likely at the bottom of the file), add it and save the file.

```
dtoverlay=w1-gpio,gpiopin=4
```

Restart your Pi for the changes to take effect.

```
$ sudo reboot
```

To start the temperature sensor read interface we need to run two
commands. Go to a command prompt on your Pi or SSH into your Pi. Type the following commands:

```
$ sudo modprobe w1-gpio
$ sudo modprobe w1-therm
```

The output of your temperature sensor is now being written to a file on your Pi. To find that file:

```
$ cd /sys/bus/w1/devices
```

In this directory, there will be a sub-directory that starts with “28-“. What comes after the “28-” is the serial number of your sensor. cd into that directory. Inside this directory, a file named w1_slave contains the output of your sensor. The contents of this file will look something like this (you can use nano to view the contents of the file):

```
￼a2 01 4b 46 7f ff 0e 10 d8 : crc=d8 YES 
a2 01 4b 46 7f ff 0e 10 d8 t=26125
```

The number after “t=” is the number we want. This is the temperature in 1/1000 degrees Celsius (in the example above, the temperature is 26.125 C). We just need a simple program that reads this file and parses out that number. We will get to that in just a second.

> Tip: if you don't see a sub-directory that starts with "28-" but see multiple sub-directories that start with "00-", you might have the resistor plugged into ground instead of into power. If your circuit is wired correctly and you continue to get "00-" sub-directories, you might have a bad temperature sensor. 


[<< Part 4: Hardware Setup](Part-4.-Hardware-Setup) - [Part 4: Initial State >>](Part-4.-Initial-State)