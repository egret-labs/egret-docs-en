In large game projects, we may design the same animation for different characters.In this case, DragonBones animation reuse can be used to easily achieve this requirement.

The animation reuse function is able to copy the animation data of the same name skeleton from one skeleton to another skeleton.

The animation codes of the two bones playing normally are as follows:

```
let egretFactory = dragonBones.EgretFactory.factory;

egretFactory.parseDragonBonesData(RES.getRes("DragonBonesDataA"));
egretFactory.parseTextureAtlasData(RES.getRes("TextureAtlasDataA"), RES.getRes("TextureAtlasA"));

egretFactory.parseDragonBonesData(RES.getRes("DragonBonesDataB"));
egretFactory.parseTextureAtlasData(RES.getRes("TextureAtlasDataB"), RES.getRes("TextureAtlasB"));

// let armatureDisplayA = egretFactory.buildArmatureDisplay("armatureA");
// this.addChild(armatureDisplayA);
// armatureDisplayA.x = 200;
// armatureDisplayA.y = 300;
// armatureDisplayA.scaleX = 0.5;
// armatureDisplayA.scaleY = 0.5;

let armatureDisplayB = egretFactory.buildArmatureDisplay("armatureB");
this.addChild(armatureDisplayB);
armatureDisplayB.x = 200;
armatureDisplayB.y = 300;
armatureDisplayB.scaleX = 0.5;
armatureDisplayB.scaleY = 0.5;

egretFactory.copyAnimationsToArmature(armatureDisplayB, "armatureA");

armatureDisplayB.animation.play("animationName");
```

Using  `Factory` in `copyAnimationsToArmature` method can achieve the effect.
`copyAnimationsToArmature` ，the first parameter of the method is the skeleton that receives the animated data, and the second parameter is the skeleton name of the copied animated data.

You can visit the sample center to see the effects of the reference samples and download the source code:
* [DragonBones online demo](http://www.dragonbones.com/demo/egret/animation_copy_test/index.html)
* [DragonBones case source code](https://github.com/DragonBones/DragonBonesJS/blob/master/Egret/Demos/src/demo/AnimationCopyTest.ts)