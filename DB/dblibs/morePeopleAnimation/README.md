DragonBones system allows you to create multiple skeletal animations,Users can create multiple factories to manage different bone animations, or they can use the same Factory to manage multiple bone animations.
* When using a Factory, care needs to be taken to avoid duplicate names for keel data or skeleton data.
*  It is not recommended to use more than one Factory instance without special requirements

Use more than one EgretFactory method, refer to the section about creating a skeletal animation.
Examples are as follows:

```
let dragonbonesData = RES.getRes( "RobotGame_1_json" );
let textureData = RES.getRes( "texture_json" );
let texture = RES.getRes( "texture_png" );

// 
let egretFactoryA = new dragonBones.EgretFactory();
egretFactoryA.parseDragonBonesData(dragonbonesData);  
egretFactoryA.parseTextureAtlasData(textureData, texture);

let armatureDisplayA = egretFactoryA.buildArmatureDisplay("robot");
this.addChild(armatureDisplayA);
armatureDisplayA.x = 200;
armatureDisplayA.y = 300;
armatureDisplayA.scaleX = 0.5;
armatureDisplayA.scaleY = 0.5;

// 
let egretFactoryB = new dragonBones.EgretFactory();
egretFactoryB.parseDragonBonesData(dragonbonesData);  
egretFactoryB.parseTextureAtlasData(textureData, texture);

let armatureDisplayB = egretFactoryB.buildArmatureDisplay("robot");
this.addChild(armatureDisplayB);
armatureDisplayB.x = 250;
armatureDisplayB.y = 350;
armatureDisplayB.scaleX = 0.5;
armatureDisplayB.scaleY = 0.5;
```

The effect is as follows:

![](56c314eb7853f.png)

Use the same Factory method as follows:

```
let dragonbonesDataA = RES.getRes( "RobotGame_1_json" );
let textureDataA = RES.getRes( "texture_json" );
let textureA = RES.getRes( "texture_png" );

let dragonbonesDataB = RES.getRes("Dragon_json");
let textureDataB = RES.getRes("dragontexture_json");
let textureB = RES.getRes("dragontexture_png");

let egretFactory = dragonBones.EgretFactory.factory;
egretFactory.parseDragonBonesData(dragonbonesDataA);  
egretFactory.parseTextureAtlasData(textureDataA, textureA);
egretFactory.parseDragonBonesData(dragonbonesDataB);  
egretFactory.parseTextureAtlasData(textureDataB, textureB);

let armatureDisplayA = dragonbonesFactory.buildArmatureDisplay("robot");
this.addChild(armatureDisplayA);
armatureDisplayA.x = 200;
armatureDisplayA.y = 300;
armatureDisplayA.scaleX = 0.5;
armatureDisplayA.scaleY = 0.5;

let armatureDisplayB = dragonbonesFactory.buildArmatureDisplay("Dragon");
this.addChild(armatureDisplayB);
armatureDisplayB.x = 250;
armatureDisplayB.y = 350;
armatureDisplayB.scaleX = 0.5;
armatureDisplayB.scaleY = 0.5;
```

The effect is as follows:

![](56c314eba5994.png)
