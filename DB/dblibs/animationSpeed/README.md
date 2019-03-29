Sometimes in the running process of the game, the need to change the dynamic animation speed. DragonBones provides several different ways to achieve variable speed animation in different scenes.

* First: adjust the animation speed

The adjustment of the clock is generally to affect a set of animations. DragonBones provides a more direct interface if you want to adjust the playback speed of an animation directly. Directly adjust the timeScale property in the animation.

```
let armatureDisplay = factory.buildArmatureDisplay("Dragon");
armatureDisplay.animation.timeScale = 0.5;
```

* Second: adjust the animation state speed

Adjusting the animation speed affects all animation states. If you only want to adjust the speed of one AnimationState in the character animation, you need to operate on the AnimationState instance generated after playing the animation.

```
let armatureDisplay = factory.buildArmatureDisplay("Dragon");
armatureDisplay.play("walk").timeScale = 0.5;
```

You can visit the sample center to see the effects of the reference samples and download the source code:
* [DragonBones online demo](http://dragonbones.com/demo/index.html)
* [DragonBones case source code](https://github.com/DragonBones/DragonBonesJS/tree/master/Egret/Demos)

 

