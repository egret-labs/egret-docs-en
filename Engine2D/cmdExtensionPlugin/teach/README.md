# Plug-in Use Case Tutorial

## The introduction

This article does not go into the details of each plug-in, but only shows how to use it. If you are interested in the details, you can refer to it [API documentation](http://developer.egret.com/cn/github/egret-docs/Engine2D/cmdExtensionPlugin/api/index.html)。

To make it easier for developers to use Egret's built-in plug-ins, we'll illustrate the Egret usage and Egret considerations in a case study.**This article is based on engine 5.2.7. Engines below this version may have some features invalid **

todosJust to write this article case from a completed project [eui cards](http://bbs.egret.com/thread-50009-1-1.html) has published to the micro letter little game, in order to make the code package **is smaller**， **better management**，gradually adding use different plug-ins, in order to realize the different needs.[Source file download address](http://tool.egret-labs.org/DocZip/engine/plugin-egret-eui-demo2.zip)
### todos

* Use the UglifyPlugin to obfuscate code compression
* Use the ResSplitPlugin to separate some resources
* Zip the file into zip format using the ZipPlugin
* Using TextureMergerPlugin incorporating texture, and then the changes in ConvertResConfigFilePlugin res. Json config file



## Project initialization

1. The index of HTML`data-scale-mode` into `fixedWidth`
2. Open EgretLauncher and publish the project as a WeChat mini-game
3. Open the WeChat developer tool



## Compress the code using the UglifyPlugin

In micro letter developer tools as you can see, the js folder five library files and a`main.js`.

Demand is now is to put the library files compressed into a file`lib.min.js`.

Go back to EgretWing and edit the config.wxgame.ts under sctipts:

```typescript
//*** other code***
//

if (command == 'build') {
    return {
        outputDir,
        commands: [
            // Clean up the js, resource folder
            new CleanPlugin({ matchers: ["js", "resource"] }),
            new CompilePlugin({ libraryType: "debug", defines: { DEBUG: true, RELEASE: false } }),
            new ExmlPlugin('commonjs'), // Non-eui projects turn this setting off
            new WxgamePlugin(),

            //  Compression plug-ins
            new UglifyPlugin([
                {	
                    // Files that need to be compressed
                    sources: [
                        "libs/modules/egret/egret.js",
                        "libs/modules/eui/eui.js",
                        "libs/modules/assetsmanager/assetsmanager.js",
                        "libs/modules/tween/tween.js",
                    ],
                    // Compressed file
                    target: "lib.min.js"
                }
            ]),

            new ManifestPlugin({ output: 'manifest.js' })
        ]
    }
    }

//
// ***Other code***
```

After saving, execute in the terminal:

```shell
egret build
```

You can see the released code in the WeChat developer tool. The library files in the js folder have been compressed to lib.min.js.

But an error, can not find the eui, this is because the automatically generated  `manifest.js` In the face of js reference sequence in js  error, need priority reference lib. Min. Js

Open the root directory of `manifest.js`， modify the reference sequence.

```javascript
require("js/lib.min.js")
require("js/main.js")
require("js/default.thm.js")
```

Each time you compile `manifest.js` can be regenerated, so we use a custom script to modify their order

Open scripts under myplugin.ts:

```typescript
/**
 * See the sample custom plug-in:http://developer.egret.com/cn/2d/projectConfig/cmdExtensionPluginin/ 
 * Learn how to develop a custom plug-in
 */
export class CustomPlugin implements plugins.Command {
    private buffer
    constructor() {
    }

    async onFile(file: plugins.File) {
        // Save the contents of the manifest.js file
        if(file.basename.indexOf('manifest.js') > -1) {
            this.buffer = file.contents
        }
        return file;
    }

    async onFinish(commandContext: plugins.CommandContext) {
        // Move 'lib.min.js' to the first place
        
        if (this.buffer) {
            let contents: string = this.buffer.toString()
            let arr = contents.split('\n')
            let lib
            arr.forEach((item, index) => {
                if (item.indexOf('lib.min.js') > -1) {
                    lib = item
                    arr.splice(index, 1)
                }
            })
            if (lib != null) {
                arr.unshift(lib)
            }

            let newCont = arr.join('\n')
            commandContext.createFile('manifest.js', new Buffer(newCont))
        }
    }
}
```

 This file is customized by the plug-in. It is already referenced by default in config.wxgame.ts, so you only need to call it

```typescript
new ManifestPlugin({ output: 'manifest.js' }),
// Called after the manifest.js is generated
new CustomPlugin()
```





## Use the ResSplitPlugin to separate the resource files

Because WeChat has a limit on the size of code package, the total size cannot exceed 4M (the subcontract function can be improved to 8M),so we need to separate some game resource files through ResSplitPlugin, put the game resource on an external CDN server, and load it dynamically when needed.。

Edit config.wxgame.ts：

```javascript
// ***other code***
//

new ResSplitPlugin({
    verbose: false, matchers:
    [
        // from USES glob expressions to match files, and projectName is the name of the project
        { from: "resource/art/about/**.**", to: `${projectName}_wxgame_remote` },
        { from: "resource/art/heros_goods/**.**", to: `${projectName}_wxgame_remote` }
    ]
})

// ***other code***
```

After saving, execute in the terminal:

```shell
egret build
```

Micro letter resource in the developer tools > art under the `about` and `heros_goods`is already gone.

In the root directory of the Egret project is separated out `egret-eui-demo_wxgame_remote` folder.



* Node 1：developers need to write their own logic to determine which resources are loaded remotely and which are stored locally in a WeChat game
* Node2：  in order to facilitate debugging, we put resources in the Egret project root directory `egret-eui-demo_wxgame_remote` folder, the general on CDN.



## Use the ZipPlugin to zip the file

In order to reduce the loading times and transfer amount, we can compress the file into zip format, and use the third-party library JSZip to read the used zip file.

Before using the ZipPlugin, you need to install cross-zip and cross-zip-cli, and type in the terminal:

```shell
//Global installation
npm install cross-zip -g   
npm install cross-zip-cli -g
```
After the installation is complete, add the code in config.wxgame.ts:

```typescript
new ZipPlugin({
    mergeSelector: p => {
        // if the file is under assets/ path, zip it to assets.zip
        if (p.indexOf("assets/") >= 0) {
            return "assets.zip"
        }
    }
})
```

In fact, the resources in the project assets are not used, here we use it to demonstrate the use of the compression plug-in.

After saving, execute in the terminal:

```shell
egret build
```

After execution, you can see in the WeChat developer tool that the original assets folder has been compressed into assets.zip under the resource directory.



## Use TextureMergerPlugin, ConvertResConfigFilePlugin combined texture packs

The image resources used in the project are all separate PNG files, and each image is requested separately at load time.We can reduce the number of requests by combining the texture sets to create a single image.
Before using the plug-in, we need to have the texture of configuration file `tmpropject`， can be generated by two ways:

1. Install the [TextureMerger](https://egret.com/downloads/texture.html)
2.  Execute script generation

To use the second method, use the script automerger. js:

```js
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
var fs = require("fs");
var path = require("path");
var resjsons = ["resource/default.res.json"]; // The res.json file to scan
var targetDir = "resource/TextureMerger"; //output directory
var pathNor = path.relative(targetDir, "resource"); //returns a relative path
var tempindex = 0;
//create the output folder
if (resjsons.length > 0) {
    if (!fs.existsSync(targetDir)) {

        // var paths = path.normalize(targetDir).split("\\");   //use in windows 
        var paths = path.normalize(targetDir).split("\/");   //use in mac linux 

        var target = ".";
        for (var _i = 0, paths_1 = paths; _i < paths_1.length; _i++) {
            var p = paths_1[_i];

            // target += ("\\" + p);  //use in windows
            target += ("\/" + p);  // use in mac linux

            if (!fs.existsSync(target))
                // create folders by path
                fs.mkdirSync(target);
        }
    }
}
var _loop_1 = function (resJson) {
    // determine if it is a res.json file
    if (fs.existsSync(resJson) && resJson.indexOf("res.json") > -1) {
        var defaultJson = fs.readFileSync(resJson, "utf-8");
        // Parse the contents of the res.json file
        var defaultObject = JSON.parse(defaultJson);
        var groups = defaultObject.groups; //group
        var resources = defaultObject.resources; //resources
        var resourcesHash_1 = {}; // The resource information to hold resources

        // Traverse resources
        for (var _i = 0, resources_1 = resources; _i < resources_1.length; _i++) {
            var resource = resources_1[_i];
            resourcesHash_1[resource.name] = resource.url;
        }

        // Traverse groups
        for (var _a = 0, groups_1 = groups; _a < groups_1.length; _a++) {
            var group = groups_1[_a];
            var tmproject = {}; // tmproject file configurationInformation used to store tmproject files
            // tmproject file configuration
            tmproject["options"] = {
                "layoutMath": "2",
                "sizeMode": "2n",
                "useExtension": 1,
                "layoutGap": 1,
                "extend": 0
            };
            // projectName
            tmproject["projectName"] = group.name + "_" + tempindex; 
            //  version
            tmproject["version"] = 5;
            tempindex++;

            // Get the keys of the res.json group and split them into arrays
            var oldkeys = group.keys.split(","); 
            var oldkeysHash = {};
            // Traverse oldkeys
            for (var _b = 0, oldkeys_1 = oldkeys; _b < oldkeys_1.length; _b++) {
                var key = oldkeys_1[_b];
                // Save to the oldkeysHash object
                oldkeysHash[key] = true;
            }

            var newKeys = [];
            // Traverse oldkeys
            for (var _c = 0, oldkeys_2 = oldkeys; _c < oldkeys_2.length; _c++) {
                var key = oldkeys_2[_c];
                if (key.indexOf("json") == -1) {
                    if (!oldkeysHash[key.replace("png", "json")]) { //the atlas of particles and keel doesn't fit
                        if (!oldkeysHash[key.replace("png", "fnt")]) //bitmap font 
                            newKeys.push(key);
                    }
                    else if (key.indexOf("jpg") > -1) {
                        newKeys.push(key);
                    }
                }
            }
            oldkeysHash = {};
            oldkeys = [];
            // files path
            var urls = newKeys.map(function (key) {
                return path.join(pathNor, resourcesHash_1[key]);
            });
            tmproject["files"] = urls;
            // write the file according to tmproject 
            if (urls.length > 0) {
                fs.writeFileSync(path.join(targetDir, tmproject["projectName"] + ".tmproject"), JSON.stringify(tmproject));
            }
            tmproject = {};
        }
    }
};
//start the scan according to the array
for (var _a = 0, resjsons_1 = resjsons; _a < resjsons_1.length; _a++) {
    var resJson = resjsons_1[_a];
    _loop_1(resJson);
}


```

Put this script in the scripts folder, the script is based on project `default.res.json`  file to generate the content of the `tmpropject` files.

Execute in the terminal:

```shell
node scripts/autoMerger.js
```
After successful execution may be a more see in the resource folder TextureMerger folder, it is according to`default.res.json` grouping generated  `tmpropject` files.

For now, the TextureMergerPlugin is only needed to perform the TextureMergerPlugin. Note that the TextureMergerPlugin is dependent on the TextureMerger version 1.7 or above. If it does not conform, please install it yourself and the TextureMerger needs to be turned off at run time.

```typescript
new TextureMergerPlugin({textureMergerRoot:[ 'resource']})
```

After saving, execute in the terminal:

```shell
egret build
```

After the execution, you can see in the WeChat developer tool that three new PNG files have been added to resource > TextureMerger, which is the combined texture set.When the game is running, you only need to load these three texture sets. You don't need to load those separate PNG files, but you need to configure them in res.json.

These operations, of course, do not need to complete manually, now only need to use ConvertResConfigFilePlugin plug-in can achieve this function.

Edit config.wxgame.ts：

```typescript
new TextureMergerPlugin({textureMergerRoot:[ 'resource']})

new ConvertResConfigFilePlugin({
    resourceConfigFiles: [{ filename: "resource/default.res.json", root: "resource/" }],
    nameSelector: (p) => {
         return path.basename(p).split(".").join("_")
    },
    TM_Verbose: true
})
```

After saving, execute in the terminal:

```shell
egret build
```

In the WeChat developer tool, open the debugger and see the loaded texture set in the network panel.

Here is a note, click the hero button in the game, switch to the hero scene, you will find that the list of pictures can not load out.

In the network panel, you can see that the load request is a separate PNG file rather than a texture set.

This is because the address of the image in the list is directly using the url.

```typescript
// Primitive array
let dataArr:any[] = [
    {image: 'resource/art/heros_goods/heros01.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: false},
    {image: 'resource/art/heros_goods/heros02.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: false},
    {image: 'resource/art/heros_goods/heros03.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: true},
    {image: 'resource/art/heros_goods/heros04.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: false},
    {image: 'resource/art/heros_goods/heros05.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: false},
    {image: 'resource/art/heros_goods/heros06.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: false},
    {image: 'resource/art/heros_goods/heros07.png', name: '亚特伍德', value: '评价: 很特么厉害, 为所欲为', isSelected: false}
]
// Convert to eui data
let euiArr:eui.ArrayCollection = new eui.ArrayCollection(dataArr)
// Set the list_hero data source to euiArr
this.list_hero.dataProvider = euiArr
// Set the item visualizer for list_hero (write the class name instead of the instance)
this.list_hero.itemRenderer = heroList_item
```

This way of referring to the image, the developer needs to manually modify the code to modify the image address into the texture set of the image.



## Conclusion

In this paper, through the use of UglifyPlugin, ResSplitPlugin ZipPlugin, TextureMergerPlugin, ConvertResConfigFilePlugin plugin.Reduce the size of the code package after the project is published to the WeChat applet, reduce the number of user initiated requests, and confound the code.

Using Egret's own plug-ins can already meet the basic needs of developers, if you have specific needs for the project, you can choose [custom plug-in](http://developer.egret.com/cn/github/egret-docs/Engine2D/cmdExtensionPlugin/plugin/index.html).

