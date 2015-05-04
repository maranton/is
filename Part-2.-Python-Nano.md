When you logged into your Pi, you landed in the /home/pi directory. To see a list of subdirectories and files in this directory, enter the command:

```
$ ls
```

This will “list” everything in the current directory.

```
￼pi@raspberrypi ~ $ ls
Desktop piot python_games streamer
```

For the Pi that you are using at the workshop, there will be a directory called “piot” listed (if you are repeating this workshop at home on a new Pi, you will need to create this directory using the command “git clone https://github.com/InitialState/piot-101.git”). We want to navigate into this directory by typing the following:

```
$ cd piot
```

`cd` will “change directory”. You can type `cd ..` to return to the parent directory that you just came from (if you do, cd back into the piot directory). Type “ls” to see all of the files in this directory. You will notice several files that end in `.py`. These are the Python scripts that you will be modifying and running throughout this workshop. These scripts are how we will tell the Pi what to do.

> *Note: Python is a very popular, high-level programming language that is commonly used by the Pi community. The purpose of this workshop is not to teach you Python but to introduce you to Python. If you are interested in learning more about Python, I recommend taking the free, online Python introductory course at http://www.codecademy.com (this is an awesome site for learning the basics of Python and other languages at your own pace).*

For this workshop, we need to know how modify and run an existing Python script. Let’s create our first Python script using the simple command-line text editor, nano. Run the following:

```
$ nano hello.py
```

Nano will be invaluable for creating and modifying our Python scripts as well as other text files on our Pi. You can navigate up, down, left, and right using the arrow keys. To enter text at the current cursor position, simply start typing. You can easily copy and paste text inside of nano (edit -> copy/paste). This means you can copy text from this guide on your laptop and remotely paste it into a file on your Pi through nano ... quite handy.

Once you have loaded nano, enter the following line of Python code:

```python
print "Hello World!"
```

Yep, we are creating the cheesy, predictable “Hello World” program as our first Python script. To save your changes, click`CTRL`+`x`, then `y`, then enter. Notice that you are responding to the prompts at the bottom of the screen to save your file.

We are now ready to run our first Python script. At the command prompt, type:

```
$ python hello.py
```

> *Note: Just like this workshop is an introduction to Python, it is also just an introduction the using a Linux command line shell. To learn more command line magic, check out http://linuxcommand.org/learning_the_shell.php.*


[<< Part 2. SSH](Part-2.-SSH) - [Part 3. Buttons & Lights >>](Part-3.-Buttons-&-Lights)