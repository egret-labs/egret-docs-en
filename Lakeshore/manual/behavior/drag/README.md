![](564d7e8d64902.png)

An instance applied the drag-and-drop behavior can be dragged by a mouse or finger (mobile device).

### Properties pane：
![](56331c9e8e7f0.png)
- Direction: sets the direction that allows dragging. Default: arbitrary. Options are:
 - Arbitrary: means that any backward drag and drop can be carried out in the game interface plane.
 - Horizontal: indicates that it can only be dragged in the horizontal direction, which means the X-axis direction.
 - Vertical: indicates that you can only drag in the vertical direction, which is the Y-axis direction.
- Enable: sets whether drag is available when game is initialized. The default value is: yes. You can also set it to "no" and then enable drag-and-drop behavior based on specific conditions in the event table.

------------

### Drag conditions：
![](56331c9ea106b.png)
#### If Drag：
Determines whether the current instance is being dragged. 【Persistent trigger】
If it is being dragged, the condition is true.
This condition has no property setting window.

#### Start drag：
When the drag starts. 【 one-time trigger 】
The moment when the drag begins.
This condition has no property setting window.

#### End drag：
When the drag ends. 【 one-time trigger 】
The moment when the drag finishes.
This condition has no property setting window.

------------

### Drag Action：
![](56331c9e4e8f4.png)
#### Enable/Disable：
Set whether the drag behavior is available.
![](56331c9e75218.png)