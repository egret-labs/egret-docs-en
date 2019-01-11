![](56430c39f2708.png)
### Magic square intro
For a beauty look in game, some rounded rectangles or irregularly shaped rectangles are often used.
Such as the image shown as below:
![](56430ddea2d0c.png)
We can use this rounded rectangle as the background of a text box. Shown as below:
![](5643103726bc4.png)
But if the text content is dynamic and a lot, it may be necessary to stretch this rounded rectangle. Here if you don’t use magic squares tech, it may occur the following condition:
![](564311a7a1fb2.png)
As we can see, the rounded corners are deformed which is not good-looking.
If we use magic square tech on rounded rectangle of background, we will get the following effect:
![](5643127eb80b4.png)

------------


### Unique property panel：
![](564318db6a6ff.png)
- Image source: image address used magic square.
- Configuration data: configuration data of magic squares. The default value is (0,0,0,0)
The format is（X,Y,Width,Height)
Here the X and Y represent the coordinates of the intersection of the upper left corner of the crisscross line.
Width and Height respectively represent the width and height of rectangle area at the center of the crisscross line. It’s shown as below:
![](56498d78cf5a2.png)
Fill in the configuration data, and do any stretch action to the magic squares image, it would not be deformed due to stretching.
- Enabled in collision: set whether the magic square instance is enabled with collision or not.

In game, the magic square instance is able to scale its size through dynamic state and action, and won’t be deformed in the meantime.

------------


### Magic square conditions
There are no special conditions for magic square components, and it applies all general conditions. Please refer to: [general conditions](../../../../Lakeshore/manual/commonElements/conditions/README.md)

------------


### Magic square actions
There are no special actions for magic square components, and it applies all general actions. Please refer to: [general conditions](../../../../Lakeshore/manual/commonElements/action/README.md)