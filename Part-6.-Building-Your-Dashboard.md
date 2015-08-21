Go to your Initial State account and you should see a new data bucket named "💻 sensors". The first thing to notice is that your bucket name has an emoji in it. Look at line 9 of sensors.py:

```python
BUCKET_NAME = ":computer: Sensors"
```

The ```:computer:``` part of the bucket name is an emoji token that gets replaced with the actual emoji when displayed. You can get a list of all emoji tokens at [http://emoji.codes](http://emoji.codes). You can use emoji tokens in bucket names, signal/stream names, and signal/stream values. This is important because emojis can convey context efficiently, most commonly with just a single character. When creating a data visualization such as a dashboard, efficiently communicating context, emotion, urgency, etc. is not only important, it is fun 😎.  

Click on the "💻 sensors" data bucket and select the Tiles visualization. You will see something similar to the following the first time you load a new bucket in Tiles:

![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard3.jpg)

Congratulations, you just created a real-time dashboard (well that was easy, wasn't it?). Every signal/stream coming into that data bucket has a tile automatically created for it. This gives you a single view where you can see all of your data at-a-glance. You just need to customize how each tile is drawn, the size of each tile, and the order that you want the tiles to be in.

Let's start with resizing a tile. Simply click on any corner or edge of a tile and drag to resize it as a square or rectangle. Wide rectangles are useful for signals/streams that have a line graph drawn like the two temperatures.

Now let's re-order our tiles. Click on the name of the tile and drag to move the entire tile to another slot. Notice how tiles won't overlap but auto-pack. You can make your dashboard look something like this by changing tile sizes and order:

![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard4.jpg)

Let's make one more tweak. Let's change the tile type. Mouse over the cog icon in the top right corner of the 🚪 Door tile to see a list of available types. Change the tile type to bar chart, pie chart, and histogram to see the different types. The pie chart and bar chart give you different views for how long the 🚪 Door stream has each value (in this case either Open or Close). The histogram shows you when an "event" happened for 🚪 Door. The histogram is particularly useful when you simply want to see when or how often something happened in the 🚪 Door stream. The "last value" type is pretty self-explanatory, useful when you only care what is happening not what happened. For the last value type, notice the text at the bottom of the tile "Since Aug 18, 2015 2:12:06 PM". This tells you when the last event happened, often a helpful piece of information.

![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard5.jpg)

I am sure you noticed that you have not only your two temperature streams and a door stream but also a fourth stream named Status. Status isn't the output of a sensor, but a stream that our script created. Lines 49-54 of sensors.py drives this stream based on the temperature from the sensor:

```python
        if temp_f > TEMPERATURE_TOO_HIGH_F:
            streamer.log("Status", ":fire:")
        elif temp_f < TEMPERATURE_TOO_LOW_F:
            streamer.log("Status", ":snowflake:")
        else:
            streamer.log("Status", ":thumbsup:")
```

If the temperature gets too warm, Status changes to :fire: (TEMPERATURE_TOO_HIGH_F is set on line 12, feel free to change this number and restart the script). If the temperature gets too cold, Status changes to :snowflake: (TEMPERATURE_TOO_LOW_F is set on line 13). If the temperature is neither too high or low, a :thumbsup: is sent. Heat up the temperature sensor in your hand and cool it down in ice to see the dashboard and the status tile update in real-time.

![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dasboard6.jpg)

[<< Part 6: Stream It](Part-6.-Stream-It) - [Part 6: Conclusion and Next Steps >>](Part-6.-Conclusion-And-Next-Steps)