###Step 11: Configure Resolution
You may have noticed that the GUI is not stretched across the full width of the LCD. This is because you have to manually specify the resolution of this LCD to your Pi. To do this, you will need to modify a configuration file, `/boot/config.txt`. The simple command line editor that will be used throughout this workshop is a program called nano.

At a command prompt, type `sudo nano /boot/config.txt` and hit enter. The “sudo” part of the command allows you to run commands as a “super user” with administrator privileges. This is a requirement for modifying the /boot/config.txt file. The “nano” part of the command starts the nano program to modify /boot/config.txt.Use the arrow keys to navigate the blinking cursor to desired location. Make the following modifications/additions to the file:

```
# uncomment if hdmi display is not detected and composite is being output
hdmi_force_hotplug=1# uncomment to force a specific HDMI mode (here we are forcing 800x480!)
hdmi_group=2hdmi_mode=1hdmi_mode=87hdmi_cvt 800 480 60 6 0 0 0
```

Once complete, hit `CTRL` + `x`, then `y`, then enter to save the file. If you made a
mistake and do not want to save your changes, hit `CTRL` + `x`, then `n`, then enter to exit without saving your changes.

###Step 12: Increase USB Power
Since we are going to power the LCD from the USB port of the Pi, we need to make another change to our /boot/config.txt file to provide enough power to drive the LCD, the wireless keyboard/mouse receiver, and a WiFi adapter (or other peripheral). Type sudo nano /boot/config.txt and hit enter. Add the following line to the bottom of this file:

```
max_usb_current=1
```

Save your changes (`CTRL` + `x`, `y`, then enter).

###Step 13: Reboot
Setup is almost complete. We simply need to reboot our Pi to ensure the LCD setup changes worked. At a command prompt, type `sudo reboot` and hit enter. Shutting down or rebooting your Pi requires the ‘sudo’ privilege prefix. Once reboot completes, your LCD should be full screen when you go into the GUI (`startx`).

###Step 14 (optional): WiFi Setup
If you are going to use a WiFi adapter instead of a wired Ethernet connection, plug the adapter into an available USB port. Start the GUI (startx) and launch the WiFi config under Menu -> Preferences to go through the WiFi setup.

[<< Part 1: Initial Setup](Part-1.-Initial-Setup) - [Part 2: Hello World >>](Part-2.-Hello-World)