DragonBones itself does not implement event dispatch. The dispatch and receive of animation events and custom events are dependent on the event system of the engine.This allows DragonBones events to be integrated into the event systems of the supported engines.

In Egret, DragonBones relies on Egret maturedisplay to send and receive events, so we listen in on events.You can receive all animation events and custom events from the framework (please refer to the tutorial and documentation for more information about Egret events).。

[dragonBones.EventObject](http://developer.egret.com/cn/apidoc/index/name/dragonBones.EventObject) defines the types of events related to dragonBones,He also through to the event listener as an event parameter [dragonBones.EgretEvent](http://developer.egret.com/cn/apidoc/index/name/dragonBones.EgretEvent) 。

The code is as follows:

```
let armatureDisplay = factory.buildArmatureDisplay("armatureName");
this.addChild(armatureDisplay);

// Event listener.
function animationEventHandler(event: dragonBones.EgretEvent): void {
    let eventObject = event.eventObject;
    console.log(eventObject.animationState.name, event.type, eventObject.name ? eventObject.name : "");
}

// Add animation event listener.
armatureDisplay.addEventListener(dragonBones.EventObject.START, animationEventHandler, this);
armatureDisplay.addEventListener(dragonBones.EventObject.LOOP_COMPLETE, animationEventHandler, this);
armatureDisplay.addEventListener(dragonBones.EventObject.COMPLETE, animationEventHandler, this);
armatureDisplay.addEventListener(dragonBones.EventObject.FADE_IN, animationEventHandler, this);
armatureDisplay.addEventListener(dragonBones.EventObject.FADE_IN_COMPLETE, animationEventHandler, this);
armatureDisplay.addEventListener(dragonBones.EventObject.FADE_OUT, animationEventHandler, this);
armatureDisplay.addEventListener(dragonBones.EventObject.FADE_OUT_COMPLETE, animationEventHandler, this);

// Add animation custom event listener.
armatureDisplay.addEventListener(dragonBones.EventObject.FRAME_EVENT, animationEventHandler, this);

// Add animation sound event listener.
factory.soundEventManager.addEventListener(dragonBones.EventObject.SOUND_EVENT, animationEventHandler, this);
```

* Custom events can be added in the event timeline in DragonBones Pro.（[video tutorial](http://developer.egret.com/cn/article/index/id/1091)）
* Custom events can configure custom parameters.
* Sound events can be listened to uniformly through the factory's soundEventManager instance, rather than individually for each skeleton.

* [DragonBones online demo](http://www.dragonbones.com/demo/egret/animation_base_test/index.html)
* [DragonBones case source code](https://github.com/DragonBones/DragonBonesJS/blob/master/Egret/Demos/src/demo/AnimationBaseTest.ts)