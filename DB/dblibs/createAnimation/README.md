First export a skeleton animation data from DragonBones Pro. You can download it by clicking on the link below.

[Robot.zip](http://sedn.egret.com/ueditor/20150701/55937e0a59ba9.zip)

We through the Res Depot tool from the resource`texture.png`，`texture.json`and`RobotGame_1.json` added to the project team.

After loading resources using the RES module, you can create a dragonbone-based skeleton animation.

Instantiate the data required for DragonBones.

```
var dragonbonesData = RES.getRes( "RobotGame_1_json" );  
var textureData = RES.getRes( "texture_json" );  
var texture = RES.getRes( "texture_png" );
```

DragonBones animation is managed by the factory class, and you can use the EgretFactory object to handle all animation data and decals.
The steps are as follows:

1. Parse external data and add to EgretFactory
2. Sets the texture of the binding in the animation

```
let egretFactory: dragonBones.EgretFactory = dragonBones.EgretFactory.factory;
egretFactory.parseDragonBonesData(dragonbonesData);  
egretFactory.parseTextureAtlasData(textureData, texture);
```

After the data is ready, it is necessary to extract the required skeleton system from the data. In DragonBones, the skeleton consists of multiple bones. Each skeleton is bound to the current skeleton's animation data.

`let armatureDisplay: dragonBones.EgretArmatureDisplay = egretFactory.buildArmatureDisplay("robot");`

Through `buildArmatureDisplay`method, we extract the name for `robot` skeleton.To see the skeleton in the stage, we need to explicitly add it to the stage, using the following statement.

```
this.addChild(armatureDisplay);
armatureDisplay.x = 200;
armatureDisplay.y = 300;
armatureDisplay.scaleX = 0.5;
armatureDisplay.scaleY = 0.5;

armatureDisplay.animation.play("Walk");
```

`armatureDisplay` is named  `robot`skeleton object display objects. Add it to the display list and you can see the currently extracted robot in the stage. The effect is as follows:

![](56c3144fce23f.png)

If you need to play the animation name, please refer to the following figure. In DragonBones Pro, the animation panel lists all playable animation names.

![](56c314504fd66.png)

