
## Introduction

Texture Merger can combine fragmented texture into a whole image, while analyzing SWF and GIF animation, and exporting configuration file to be used by Egret.


### Adapt to the platform

* Windows
* Mac OS X

### Adaptation version

* Egret Engine version 1.6.0 and above


### download link

* [Texture Merger download address] (http://www.egret.com/downloads/texture.html)

## types

![name](qidong.png)

* Egret MovieClip: convert swf or gif animation into the related resources needed by Egret MovieClip.
* Sprite Sheet: combine the fragmented images into a big whole image.
* Bitmap Font: the resources needed to create Egret bitmap text.

### Egret MovieClip

Egret Engine 1.5.0 version adjusts the data structure of MovieClip, allowing a file to contain multiple animations. Tools are also allowed to load multiple animations, but the tools's capability of parsing the swf is poor. Currently there is still certain requirements for the SWF: swf itself must be a multi-frame mc. Drawing is not applicable for the practice of just nesting other mc sub-items in the name of container.There are almost not requirements for gif and almost all can be drawn out. However, the production methods of gif animation vary because some frames may not be fully drawn out.

![name](donghua.png)

Here we will look at the latest mc data structure:


```
MovieClip data format standard
{
  "file": "icons.png""mc": {
    "mc_name1": {
      "frameRate": 24,
      "labels": [
        {
          "name": "stand",
          "frame": 1
        }
      ],
      "frames": [
        {
          "res": "res_name1",
          "x": 3,
          "y": 0,
          "duration": 2
        }
      ],
      "actions": [
        {
          "name": "action_name1",
          "frame": 1
        }
      ],
      "scripts": [
        {
          "frame": 1,
          "func": "gotoAndPlay",
          "args": [
            "attack"
          ]
        }
      ]
    }
  },
  "res": {
    " res_name1": {
      "x": 170,
      "y": 674,
      "w": 80,
      "h": 110
    }
  }
}
```

```
"file": The texture file path corresponding to the data file  (used to help the tool to match the corresponding problem, and the engine will not parse this attribute) 
"mc": MovieClip data list, 
Each attribute in the list represents a MovieClip name
"frameRate": Frame rate, [optional attribute], the default value of 24, which can be set by the developer through the code
"labels": Frame tag list, [optional attribute]. If there is no frame tag, you can choose not to add this attribute.
"name": Tag name
"frame": The frame number where the label is located
"frame": Keyframe data list
"res": The image resources needed to be displayed on the key frame, [optional properties], the default value is empty (used for the case of blank frames)
"x": The x coordinate required to be displayed by image, [optional attribute], the default value of 0
"y": The y coordinate required to be displayed by image, [optional attribute], the default value of 0
"duration": The number of consecutive frames of the key frame, [optional attribute], the default value of 1
"actions": Frame action list, which is used to throw a custom event, [optional properties]. If there is no frame action, you can choose not to add this attribute.
"name": Action name
"frame": The frame number where the action is located
"scripts": Frame script list, [optional properties]. If there is no frame action, you can choose not to add this attribute.
"frame": The frame number where the script is located
"func": The method name of the script call, supporting six APIs related to animation playback
"args": The parameter list used by the script call method [optional attribute], the default value is empty
"res": Resource list
Each attribute in the list represents a resource name
"x": The x coordinate of the location of the texture set in the resource
"y": The y coordinate of the location of the texture set in the resource
"w": Resource width
"h": Resource height
```

> actions, scripts are not yet enabled.

### SpriteSheet

![name](SpriteSheet.png)

* The tool provides two ways to import data: import by dragging or clicking on the menu. The following status bar has the information of texture size, zoom, and the editing format.
* A quick button to view the tutorial has been added to the lower right corner. some new users do not know how to use it here.

![name](SpriteSheet_1.png)
![name](SpriteSheet_2.png)
![name](SpriteSheet_3.png)
![name](SpriteSheet_4.png)

* The configuration pf additional extension can add the file extension to the texture name. For example, Png will be added as _png, which is invalid for Egret MovieClip.
* Two automatic matching strategy: Power 2 and Free Size, the former of which can get the appropriate size of the power of 2, while the latter can get the right free size.
* Removal of transparent boundaries refers to the cutting off of all the transparent parts around the transparent image.For the specific effect, you can have a tryHere we introduce some texture material.

### Import texture material

![name](wenli.png)

* After importing the material, you can see the large texture that has been arranged. The tool on the imported texture reprocesses the imported texture. The same texture will not display repeatedly, with only the texture name left.
* The left side has the corresponding texture list and these names are consistent with the file name. Through the list you can see the location of the corresponding texture box on the big map , or you can also delete the useless texture after multiselecting via Ctrl or Shift key. You can complete such operation by deleting the option with right click.

### Save and open

![name](wenli_1.png)

* Save the currently edited texture set information as a project file, so as to make it easier to make changes in the future

### New

![name](new.png)

If you want to continue editing, click on New, and then the interface and Start interface are the same.

### Bitmap Font

The feature of making texture fonts supports three forms of loading:

* Hash single character image
* The entire character set image
* System font

The default action is the import of a single character image, which can be viewed from "other characters" in two other ways.

### character image

Single character import is relatively simple, just like the operation of SpriteSheet.

### System font

![name](xitongwenzi.png)

Here you can get the system font, and can set the font size, color, thickness, and then enter the desired characters in the input box. Please note that the space characters need to be entered.


### character set

![name](wenliwenzi.png)

Character set is generated for facilitating the more personalized fonts. It is fine for the art staff to make good arrangement for the drawn characters to import into a image, and then use the tool to import. The tool will automatically identify the area of each character. What we need to do is to fill in the corresponding text in following text box.


## Command line call

The 1.5.2 version of the TextureMerger supports simple command line calls

### Package command
* Command format: -p [directory] [...] -o [json output path] -e [regular expression for file filter]

* Command example: -p d:/Y1 d:/Y2 -o d:/yyy.json -e /.*\.(jpg|png), pack all png and jpg files under drive Y1, Y2 of disk D and output the packed file to the yyy.json of disk D.

	-e is an optional command. If it is not written, by default, all images supported by textureMerger will be packaged

### Modify the json command
* Command format: -rp [json path] -d [texture key] [...] -a [file path] [...]

* Command example: -rp d: /user/aaa.json -d head leg -ad: /user/1.png d: /user/2.png modifies the aaa.json file under the user directory of disk D, delete key as the texture of head and leg, and add 1.png and 2.png.This command covers the original file.-d and -a are optional commands

### Convert animation commands
* Command format: -mc [directory] [...] -o [output path] -e [regular expression for file filter]

* Command example: -mc d:/Y1 d:/Y2 -o d:/outpath -e /.*\.(swf|gif).Convert all swf and gif files under directories Y1 and Y2 of disk D and input the converted files to the outpath directory of disk D.

	-e is an optional command. If it is not written, by default, all animation files under the directory supported by textureMerger will be converted


## attention

The image quality is seriously degraded as the result of this tool's repeated editing of json, which is caused by the repeated encoding and decoding. Here we use a number of PNG coding library for the test

* Original image:

![name](1.png)


* The result of repeated decoding and encoding for 20 times:


![name](2.png)

![name](3.png)

> The above is the result of the implementation of two png coding library, the highest quality of which have already been enabled.You can find that the first one is relatively good, but is still much inferior to the original image. More efforts need to be made for exploring why there is such a big gap.It is recommended that instead of directly dragging the json file for editing, you'd better save it as project file, so as to make second editing for the project file 


