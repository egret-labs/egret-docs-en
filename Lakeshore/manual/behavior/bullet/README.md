![](564c29d98c132.png)

An instance that bullet behavior are applied has the behavior of moving in a specified direction at a given speed. So Bullet is a very much alike name, an instance applies the bullet behavior will move like a bullet.

### Properties pane：
![](564c28bde86d0.png)
- Speed: the default speed of the bullet, in pixels per second. The default value is 400, which represents a movement of 400 pixels per second.
- Acceleration: the acceleration at which the bullet moves. The default value is 0, and it's moving at a constant speed. It calls acceleration when the value is positive and deceleration when the value is negative.
- Gravity: When a bullet is moving, its gravitational force is fixed in the negative direction of the Y axis. For example, if the bullet is flying horizontally, its trajectory should be a parabola under the influence of gravity. The greater the gravity, the greater the curve of the parabola. When the default gravity is zero, and the bullet stays in a straight line.
- Default running angle: sets the default running angle of the bullet. The default value is 0. The running angle of the bullet is independent of the angle of the instance itself.
------------
### Bullet conditions：
![](5632e26789e81.png)
#### Comparative running speed：
Compares the bullet speed of the selected instance with the specified value. 【 continuous trigger 】
![](5632e267b0835.png)

#### Comparative running distance：
Compares the bullet distance of the selected instance with the specified value. The measurement of the running distance begins with the creation of the bullet. 【 continuous trigger 】
![](5632e267b0835.png)

------------
### Bullet movement：
![](5632e26711538.png)

#### Running speed：
Set the running speed of the bullet.
![](5632e2675db61.png)

#### Acceleration：
Set the acceleration of the bullet.
![](5632e2672b66d.png)

#### Running angle：
Set the running angle of the bullet.
![](5632e26752e15.png)

#### Gravity：
Set the force of gravity on a bullet as it moves.
![](5632e2676b271.png)

#### Enable/disable：
Set whether the bullet behavior is available.
![](5632e26738815.png)