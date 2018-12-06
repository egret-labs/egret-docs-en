## Enable Optimization Switch

**Suitable for Android and iOS support 3.2.2 or higher version**

**Features:**Enable optimizations on some features in support. And these optimizations are temporarily disabled by default and will be added directly to support when  it's stable.

**Usage**You need to modify the parameter of egret_native.featureEnable in egretInit function of native_require.js. For example, the optimization method of enabling rendering efficiency is shown as follow:
~~~
var feature = {
	cmdBatch : true
};
egret_native.featureEnable(feature);
~~~
**Parameter:**The available properties for a js object currently are:

cmdBatch: Reduce the data transfer tmes between engine and support, and improve rendering efficiency (added in 3.2.2).

Improve the rendering efficiency of a texture when it's used multiple times (addedin 3.2.4).



##	Enable the lastest update game package when the hot update address cannot be accessed

**Suitable for iOS support 3.2.2 or higher version**

**Features**Enable the latest update game when the hot update address cannot be accessed

**Usage:**Set the waiting time to access hot update address before enabling the game. And modify runGame method of ViewController, call it before enabling EgretRuntime:
 ![](p1.png)
**Parameter:**Waiting Time (Second)

##	Switch Audio Decoding Mode

**Suitable for Android Support 3.2.2 or Higher Version**

**Feature:**Select whether using PCM decoding first by default or not. It's enabled by default. In most cases, PCM decoding has a  faster speed, but we should note that the time length of some audio files are quite long.

**Usage**Use egret_native.setPcmDecodeEnable to enable or disable before calling play event.

**Parameter:**true/false


##	Set Game Background as Transparent

**Suitable for Android support 3.2.1 or higher version, iOS support 3.2.4 or higher version.**

**Feautres:**Set the game background of View as transparent.

**Usage:** 

Android：

Add properties in getGameOptions:

~~~
options.put(EgretRuntime.OPTION_GAME_GLVIEW_TRANSPARENT, "true");
~~~
**Note:**When we set the background as transparent, there will be a EditText in the scene, and we can delete it via

~~~
((ViewGroup)gameEngineView).removeViewAt(0);
~~~

Here the reason we keep this control is for compatibility with the 2.X version engine. It's a control by default in 2.X engine, and we can feel free to remove it if we use 3.0 or higher version engine.

iOS:

Add propeties for _options in runGame:

~~~
_options[@OPTION_GAME_GLVIEW_TRANSPARENT] = @"true";
~~~

##	Set game View as top-level view (Android)

**Suitable for Android support 3.2.1 or higher version.**

**Features:**Modify game View's layer

**Usage:** Modify the method of getting gameEngineView from game_engine_get_view to game_engine_get_view_set_top, and set game View as top-level.


##  Get Battery Information of Native Devices

**Suitable for Android/iOS support 3.1.4 or higher version**

**Features:** Get battery information of native devices.

**Usage：**

```javascript
var json_listene = { action: "listenDeviceInfoChanged" };
var jsonStr_listene = JSON.stringify(json_listene);
egret.ExternalInterface.call("egret.deviceInfo", jsonStr_listene);
             
egret.ExternalInterface.addCallback("egret.deviceInfo", function (message) {
        console.log("message form native : " + message);
});
var json = { action: "getCurrentBatteryInfo" };
var jsonStr = JSON.stringify(json);
egret.ExternalInterface.call("egret.deviceInfo", jsonStr);
```

