![](564c2a211ef6d.png)

An instance with a rotation behavior will spontaneously rotate at the specified speed. The center of rotation is the instance anchor point.

### Propety Panel:
![](5633052052ba6.png)
- Speed: The speed of rotation (Unit: degrees/second). Default value is 180. When the value is positive, it rotates clockwise. When the value is negative, it rotates counterclockwise.
- Acceleration: The acceleration of the rotation. The default value is 0, here it's a constant rotation. When the value is positive, it's clockwise acceleration (counterclockwise rotation is deceleration), and when the value is negative,  it's clockwise deceleration ( counterclockwise rotation is acceleration). For example, if the speed is 180 and the acceleration is -10, then the instance will rotate clockwise at 180 degrees/second, but the slower and slower. When the speed is 0, it starts to rotate counterclockwise and turns faster and faster.


------------
### Rotation Condition
There are no unique conditions for the rotation behavior.

------------
### Rotation Action
![](563305200cf38.png)
#### Rotation Speed
Set rotation speed.
![](5633052043608.png)

#### Rotation acceleration
Set rotation acceleration.
![](5633052035b49.png)

#### Enable / Disable
Set whether the rotation behavior is available.
![](563305202a1af.png)