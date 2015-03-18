![LX Terminal](img/IMG_3897.JPG)

In order to remotely log into your Pi from your laptop, you will need your Pi’s IP address. Go to your Pi’s command prompt by clicking on the LXTerminal icon at the top toolbar. Enter the command:

```
$ hostname -I
```

The IP address will be returned to the screen. Write your IP address down for use throughout this workshop. In the screenshot above, the Pi’s IP address is 10.1.101.91.

We are going to communicate with our Pi through an SSH connection from our Laptop for the rest of this workshop. SSH stands for Secure Shell and allows us to remotely log into our Pi and control it. On your laptop, open a command prompt. Replace the “#.#.#.#” with your Pi’s IP address and enter the command:

```
$ ssh pi@#.#.#.#
```

This will attempt to connect to your Pi through the specified IP address and login with the username ‘pi’. The first time you login to your Pi, you will receive a message similar to the following:

```
$ ssh pi@10.1.101.91
The authenticity of host '10.1.101.91 (10.1.101.91)'
 can't be established. RSA key fingerprint is
 b2:03:15:12:71:f2:6c:5c:2e:82:69:cc:5c:e8:81:54. Are
 you sure you want to continue connecting (yes/no)?
```

Enter `yes`, then enter your password. 
> The default password is `raspberry` for a new Pi. 

If successful, you will see something similar to the following on your screen:

```
Linux raspberrypi 3.18.5-v7+ #225 SMP PREEMPT Fri Jan 30 18:53:55 GMT 2015 armv7l
The programs included with the Debian GNU/Linux system are free software; the exact distribution terms for each program are described in theindividual files in /usr/share/doc/*/copyright.
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.Last login: Wed Feb 25 22:24:20 2015 from 10.0.0.41pi@raspberrypi ~ $
```

This means that you are now remotely connected to your Pi and ready to tell it what to do.

> **TIP**: The IP address of your Pi can change based on your router’s settings. If you try to SSH into your Pi and fail to get a connection, the Pi’s IP address may have changed. There are several ways to get the current IP address of your Pi. The most straightforward method is to hook a keyboard and monitor up to your Pi and run the hostname –I command. Your router may have a built-in web server that you can log into to see the IP addresses of all connected devices. A short article that discusses different ways to discover your Pi’s IP address can be [found here](http://www.raspberrypi.org/documentation/troubleshooting/hardware/networkin g/ip-address.md).


[<< Part 2. Hello World](Part-2.-Hello-World) - [Part 2. Python + Nano >>](Part-2.-Python+Nano)