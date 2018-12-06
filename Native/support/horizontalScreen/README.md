## Preparation

Egret's H5 project is able to generate corresponding Native project via Egret Android Support or Egret iOS Support. If you set the landscape and portrait screen and other info of a project, you need to set it in the corresponding Native project.


## Android Landscape and Portrait Screen Setting

### Setting in Java code

In Java code, you can set the rotation orientation of screen as landscape mandatorily as shown below:

```
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE)
```

The ActivityInfo could be the value as shown below:

```
ActivityInfo.SCREEN_ORIENTATION_UNSPECIFIED,//Unspecified, this is value by default. Android system will choose the right orientation by itself.
ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE,//landscape screen
ActivityInfo.SCREEN_ORIENTATION_PORTRAIT,//portrait screen
ActivityInfo.SCREEN_ORIENTATION_USER,//User's current preferred orientation
ActivityInfo.SCREEN_ORIENTATION_BEHIND,//Inherit the orientation of the Activity that's behind the current Activity of Activity stack
ActivityInfo.SCREEN_ORIENTATION_SENSOR,//The display orientation is determined by the physical sensor
ActivityInfo.SCREEN_ORIENTATION_NOSENSOR,//Ignore the physical sensor - which means the display orientation is irrelevant with the physical sensor
```

### Setting in AndroidManifest.xml

We can find AndroidManifest.xml configuration file in the proj.android directory of the generated Android project. It's a configuration file that's required for every Android project and provides various proerties to describe the metadata of the application. However, the screen orientation modification in program has a higher priority than in configuration file.

We can find the `android:screenOrientation` field in AndroidManifest.xml, it's the field of project's landscape and portrait screen configuration. It could have parameters shown as below, they are basically one-to-one correspondence with the aforementioned parameters: 

* "unspecified": the display orientation is judged by system, and the judgement strategy is device-related, so different devices will have different display orientations.

* "landscape": landscape display (width is longer than height).

* "portrait": Android Support's template setting value by default, protrait display (height is longer than width)

* "user":User's current preferred orientation

* "behind": it has same setting with the its behind Activity in Activity stack

* "sensor": it's determined by the physical sensor. the screen will switch between landscape and portrait mode if user rotates the device.

* Ignore the physical sensor, which means the screen orientation is irrelevant with rotation operations on device by user (expect for the "unspecified" setting).

#### Landscape Screen Setting

We can configure landscape screen setting of project like this:

```
android:screenOrientation="landscape"
```

then the project will have a landscape display.

#### Portrait Screen Setting

We can configure portrait screen setting of project like this:

```
android:screenOrientation="portrait"
```

### Landscape and Porprait Screen Setting in iOS Project

#### Setting in ViewController

Screen orientation setting in iOS project, we can set the orientation of rotation of the screen by using ViewController or info.plist. The setting method of ViewController has a higher priority than directly setting in info.plist. So we suggest you set it in ViewController.

You can find the related setting in template project provided by Egret iOS Support, and find the ViewController.mm in HelloEgret project, shown as the figure below:

![](569cc4287e852.jpg)

The codes are shown as below:

```
- (BOOL)isLandscape {
    // Return YES if it's landscape screen, and return NO if it's portrait screen
    return NO;
}
```

#### Setting in info.plist

We can also setting in info.plist, and find `Supported Interface Orientations`, four kinds of screen orientation are supported by default in iOS APP:

* Portrait: Normal portrait screen(top home button)

* PortraitUpsideDown: Reverse screen (bottom home button)

* LandscapeLeft:Landscape screen that starts from the upper left corner (left home button)

* LandscapeRight: Landscape screen that starts from the upper right corner (right home button)


You can also directly find info.plist file in the directory of the project, and find the `UISupportedInterfaceOrientations` and the `UISupportedInterfaceOrientations~ipad`  fields from info.plist.

You can delete the two modes of portrait screen if you want to set landscape screen, and vice versa.

> Generally, we suggest you not modify info.plist.






