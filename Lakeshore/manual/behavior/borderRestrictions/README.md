![](564d7dd767bd2.png)

An example of applying boundary limiting behavior，its scope of activity will be limited to the specified boundary range. 

### Properties Pane：
![](5636e53e4c768.png)
- Instance bound mode: instance bound out mode. Options are:
 - Instance border: sets that the outer border of an instance cannot go outside the specified bounds. For example: the constraint boundary is within the scope of the screen, and when the instance border reached the edge of the screen will not be able to move out under instance border mode.
 - Instance anchor point: sets that the instance anchor point cannot go beyond the specified bounds. Thus if it changed to instance anchor mode in the previous example, the border of the instance can go out of the screen edge, but when the instance anchor point reaches the screen edge, it can't move out any more.
- Horizontal coordinate: sets the horizontal coordinate value of the top-left coordinate point of the constraint boundary. (unit: pixels)
- Vertical coordinate: sets the vertical coordinate value of the top-left coordinate point of the constraint boundary. (unit: pixels)
- Boundary width: sets the width of the constraint boundary. (unit: pixels)
- Boundary height: sets the height of the constraint boundary. (unit: pixels)

------------

### Boundary Restrictions：
There are no specific conditions for boundary limiting behavior.

------------

### Boundary Restriction Actions：
![](5636e53e2629b.png)
#### Setting boundary parameters：
Sets the parameters of the boundary constraint.
- Instance restrictive mode：Instance limits the out-of-bounds pattern. Options are：
 - Instance border: sets that the outer border of an instance cannot go outside the specified bounds.
 - Instance anchor: sets the instance's anchor point will not be able to step out of the specified bound.
- Horizontal coordinate: sets the horizontal coordinate value of the top-left coordinate point of the constraint boundary. (unit: pixels)
- Vertical coordinate: sets the vertical coordinate value of the top-left coordinate point of the constraint boundary. (unit: pixels)
- Boundary width: sets the width of the constraint boundary. (unit: pixels)
- Boundary height: sets the height of the constraint boundary. (unit: pixels)

![](5636e53e405a3.png)