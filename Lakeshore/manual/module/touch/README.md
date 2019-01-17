![](564beb8425150.png)

After adding the touch screen component, the response to the touch operation on the mobile side can be realized. Only one touchscreen component can be added to a scene. The response to the touch operation is achieved by conditional determination of the added touch screen instance.
*Note: touch screen components do not support any basic properties other than "name". Collision is not supported. The addition of a touch screen component does not result in a visible instance in the game running scene.

### Specific Attribute
Touch screen components have no unique properties.

------------


### The Touch-screen Conditions
Touch screen components do not support any general conditions other than specific conditions.

![](564beb8412cb3.png)
#### When the touch is in progress
When the screen is in touch state. 【 continuous trigger 】
This condition will be triggered continuously if the finger keeps pressing the screen, that is, the condition is true if the finger keeps pressing the screen, otherwise it is false.
This condition has no property setting window.

#### Tap the screen
When you tap the screen. 【 one-time trigger 】
The trigger of this condition starts from the finger clicking on the screen until the finger leaves the screen. The following conditions are required for this process to be triggered:

1. The position recorded at the moment when the finger clicks on the screen is the same or slightly different from the position recorded at the moment when the finger leaves the screen.
2. There is a short time between the moment your finger leaves the screen and the moment it presses the screen. (generally about 200ms)
3. No touch movement event has occurred in this process. (that is, the finger is not moving on the screen)

This condition has no property setting window.

#### At the beginning of touch
When the touch begins. 【 one-time trigger 】
When the finger hits the screen, the condition is true and triggers once. Unlike "tap the screen," it doesn't require a finger off the screen to trigger.
This condition has no property setting window.

#### At the end of touch
When the touch ends. 【 one-time trigger 】
When the touch ends and the finger leaves the screen, the condition is true and triggers once.
This condition has no property setting window.

#### When the touch moves
When touched and moved. 【 one-time trigger 】
When a finger touches the screen and swipes it across the screen, each swipe is triggered. So even though the condition is a one-time trigger, if you keep swiping on the screen, it keeps firing.

#### When the off screen touch ends
When the touch is swiped off the screen. 【 one-time trigger 】
When the touch swipes off the screen and the touch ends, the condition is true and triggers once.

------------


### A touch screen motion
The touch screen component does not support any actions.

------------


### Expression
Touchscreen components provide unique expressions.
- touchx: represents the horizontal coordinate of the touch of a finger on the screen
- touchY: represents the vertical coordinates of a finger when touched on a screen
- touchPointID: the unique identification number assigned to the touch point when the finger is touched on the screen.

For example, if the touchscreen component is called 'touchMc', then if we want to get the horizontal coordinates of our fingers on the screen, we can say 'touchmc.touchx'.


