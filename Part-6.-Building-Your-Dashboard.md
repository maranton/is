![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard2.jpg)

Go to your Initial State account and you should see a new data bucket named "💻 sensors". The first thing to notice is that your bucket name has an emoji in it. Look at line 9 of sensors.py:

```python
BUCKET_NAME = ":computer: Sensors"
```

The ```:computer:``` part of the bucket name is an emoji token that gets replaced with the actual emoji when displayed. You can get a list of all emoji tokens at [http://emoji.codes](http://emoji.codes). You can use emoji tokens in bucket names, signal/stream names, and signal/stream values. This is important because emojis can convey context efficiently, most commonly with just a single character. When creating a data visualization such as a dashboard, efficiently communicating context, emotion, urgency, etc. is not only important, it is fun 😎.  

Click on the "💻 sensors" data bucket and select the Tiles visualization. You will see something similar to the following the first time you load Tiles:

![Dashboard](https://github.com/InitialState/piot-101/wiki/img/dashboard3.jpg)

[<< Part 6: Stream It](Part-6.-Stream-It) - [Part 6: Conclusion and Next Steps >>](Part-6.-Conclusion-And-Next-Steps)