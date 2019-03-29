DragonBones provides animation masks and animation blending capabilities for creating animation characters that are complex and flexible.Greatly reduce the designer's animation development workload, flexible control animation from the perspective of the program. For example, a character's upper body can stand up, bend over, and fire.The lower body can stand, squat and run. And the upper and lower body movements can be combined flexibly, such as the character can fire standing fire, squat fire, run fire.All of these actions are controlled in real time by the player's control.If the designer wants to design all these animations, there are 9 kinds of animations that need to be arranged and combined, which involves a lot of repetitive work,DragonBones animation mask and animation fusion features, designers only need to design 3 kinds of animation for the upper and lower body, that is a total of 6 kinds of animation, the rest of the matter to the program to achieve it.

Animation blending and animation masking are described below.

*  Animation blending
Animation blending means that one skeleton can play multiple animations at the same time. For example, the following code allows the character to play both running and firing animations.

```
armatureDisplay.animation.fadeIn("run", 0.2, 0, 0, "NORMAL_ANIMATION_GROUP");
armatureDisplay.animation.fadeIn("fire", 0.1, 1, 0, "ATTACK_ANIMATION_GROUP");
```

* Animated mask
Animation mask is to present only part of the animation. For example, the following code will play the running animation of the head and body bones, and the other bones will remain in the original position.

```
let animationState = armatureDisplay.animation.fadeIn("run");
animationState.addBoneMask("head");
animationState.addBoneMask("body_u");
```

This is implemented by AnimationState's addBoneMask API.

One thing to explain here is that DragonBones animation has a group concept at runtime,We can make the animation play in one group, when another animation is set to play in the same group, the previously played animation in the same group will stop, so we can put the animation that we want to play at the same time in different groups.
Like in the code above, we can put the firing into the upper-body group and the running into the lower-body group, so that the character can fire and run at the same time.

 Finally, the animation mask and animation are used together. The code is as follows

```
armatureDisplay.animation.fadeIn("run", 0.2, 0, 0, "NORMAL_ANIMATION_GROUP");

let animationState = armatureDisplay.animation.fadeIn("fire", 0.1, 1, 0, "ATTACK_ANIMATION_GROUP");
animationState.addBoneMask("body_u");
```
