![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard2.jpg)

Go to your Initial State account and you should see a new data bucket named "💻 sensors". The first thing to notice is that your bucket name has an emoji in it. Look at line 9 of sensors.py:

```python
BUCKET_NAME = ":computer: Sensors"
```

The ```:computer:``` part of the bucket name is an emoji token that gets replaced with the actual emoji when displayed. You can get a list of all emoji tokens at [http://emoji.codes](http://emoji.codes). You can use emoji tokens in bucket names, signal/stream names, and signal/stream values. This is important because emojis can convey context efficiently, most commonly with just a single character. When creating a data visualization such as a dashboard, efficiently communicating context, emotion, urgency, etc. is not only important, it is fun 😎.  

Click on the "💻 sensors" data bucket and select the Tiles visualization. You will see something similar to the following the first time you load a new bucket in Tiles:

![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard3.jpg)

Congratulations, you just created a real-time dashboard (well that was easy, wasn't it?). Every signal/stream coming into that data bucket has a tile automatically created for it. You just need to customize how each tile is drawn, the size of each tile, and the order that you want the tiles to be in.

Let's start with resizing a tile. Simply click on any corner or edge of a tile and drag to resize it as a square or rectangle. Wide rectangles are useful for signals/streams that have a line graph drawn like the two temperatures.

Now let's re-order our tiles. Click on the name of the tile and drag to move the entire tile to another slot. Notice how tiles won't overlap but auto-pack. 

Your dashboard could look something like this after you are done playing with sizes and order:
![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard4.jpg)

[<< Part 6: Stream It](Part-6.-Stream-It) - [Part 6: Conclusion and Next Steps >>](Part-6.-Conclusion-And-Next-Steps)