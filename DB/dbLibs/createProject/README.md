DragonBones is integrated in the installation package as an extension library to the Egret engine.If your project requires DragonBones, you will need to enable DragonBones configuration in your project configuration. The operation steps are as follows:

1、Build a new Egret project

2、Modify the egretproperties.json file in the project

In the configuration file, go to the modules TAB and add a DragonBones binding entry.

```
"name": "dragonbones"
```

The configuration content after adding is as follows:

```
"modules": [
    {
        "name": "egret"
    },
    {
        "name": "game"
    },
    {
        "name": "tween"
    },
    {
        "name": "res"
    },
    {
        "name": "dragonbones"
    }
]
```

3、Recompile the project


Recompile，please implement `egret build -e`

By doing these three steps, you can directly use DragonBones in your project.

To test the configuration for success, use the following statement for debugging. Print out the current version of DragonBones directly in the console.

```
console.log(dragonBones.DragonBones.VERSION);
```
