## 1.System information
The Egret project can be run in both HTML5 capable desktop browsers and various mobile browsers. And it can also run in an accelerated and native system environment of Egret Runtime. The information of different systems can be obtained through ` egret. "Capabilities ` class. You need to pay attention that its values are static and can be read but cannot be changed.

**Attention：** There is no gyroscope or GPS module on the computer, so that the relevant information cannot be obtained. It needs to be debugged on the phone.

### 1.1.System constant

#### egret.Capabilities.isMobile
`egret.Capabilities.isMobile` can tell if the program is running in a mobile system. Its value is a static Boolean value, and it runs in mobile system when its value access to be ` true `.

#### egret.Capabilities.language
`egret.Capabilities.language` represents the language code of the system where the content is running. Its value is the lowercase two-letter language code in ISO 639-1. Reference to [ISO 639-1](http://baike.baidu.com/link?url=me8UVbWB-oLjVT_fyxTqPwzf4cagZroNFfbiZy0Meo3VnACeZOup5vabLqoRaDwozxGm-dx600XBZRRV34pkca#2)

Special ones may be encountered as follows:

* Simplified Chinese zh-CN
* Traditional Chinese zh-TW
* English en
* Japanese ja
* korean ko

#### egret.Capabilities.os
`egret.Capabilities.os`attribute indicates the current operating system, specific possible value is as follows:

* Apple mobile operating system "iOS"
* android mobile operating system "Android"
* Microsoft mobile operating system "Windows Phone"
* Microsoft desktop operating system "Windows PC"
* Apple desktop operating system "Mac OS"
* Unkown operating system "Unknown"

#### egret.Capabilities.runtimeType
`egret.Capabilities.runtimeType` attribute can obtain type of project operation.

| Attribute values  |Corresponding constant |Corresponding type |
|:-------------|-------------|-------------:|
|web| egret.RuntimeType.WEB | Run on the browser|
|native| egret.RuntimeType.NATIVE | Runs on first-generation native projects|
|runtime2| egret.RuntimeType.RUNTIME2 | Runs on second-generation native projects|
|wxgame| egret.RuntimeType.WXGAME | Runs on WXGAMES|



### 1.2.Samples
For system information, please refer to the following code:

```
/**
 * obtain system information class
 */
class CapabilitiesTest extends egret.Sprite {

    public constructor () {

        super();

        var capabilites:Array<egret.ITextElement> = [
            {text:"mobile devices: " + egret.Capabilities.isMobile + "n",style:{size:17,"fontFamily": "Regular script"}} ,
            {text:"Language codes: " + egret.Capabilities.language + "n",style:{size:17,"fontFamily": "Regular script"}},
            {text:"Operating system: " + egret.Capabilities.os + "n",style:{size:17,"fontFamily": "Regular script"}},
            {text:"runtime type: " + egret.Capabilities.runtimeType + "n",style:{size:17,"fontFamily": "Regular script"}}
        ];

        var showCapabilities:egret.TextField = new egret.TextField();

        showCapabilities.textFlow = capabilites;

        this.addChild(showCapabilities);

    }
}
```

## 2.Gyroscope

In mobile devices, It is generally supported to obtain the rotation angle of the device itself.`egret.DeviceOrientation` can listen for the changes in the direction of the device.

### 2.1.Obtain the rotation angle of the device

The following example shows how to listen for rotation changes and get the rotation value:

```
class DeviceOrientationExample extends egret.DisplayObjectContainer {
    private label: egret.TextField;
    public constructor() {
        super();
        this.label = new egret.TextField();
        this.label.y = 50;
        this.label.x = 50;
        this.addChild(this.label);
        //Create DeviceOrientation class
        var orientation = new egret.DeviceOrientation();
        //Add event listeners
        orientation.addEventListener(egret.Event.CHANGE,this.onOrientation,this);
        //Start listening for changes in the direction of device 
        orientation.start();
    }
    private onOrientation(e:egret.OrientationEvent){
        this.label.text =
            "direction: nalpha:"+e.alpha
            +",nbeta:"+e.beta
            +",ngamma:"+e.gamma;
    }
}
```

The above code first creates the instance of `orientation`. And give it to add an event listener, listen to its `CHANGE` events. Then call his `start()` way to start monitoring equipment in the direction of change.

After listening to the change of direction, the system will callback function `onOrientation`.Then it will obtain the equipments' changes in direction through three properties of ` egret. OrientationEvent ` events.

Three properties of `OrientationEvent`：`alpha`,`beta` and `gamma`.

* `alpha` stands for the angle of the device around the Z-axis，unit in degree, range from 0 to 360.

* `beta` stands for the angle of the device around the X-axis，unit in degree, range from -180 to 180. This value represents the rotation status of the device from front to back.


* `gamma` stands for the angle of the device around the Y-axis，unit in degree, range from -90 to 90. This value represents the rotation status of the device from left to right.


## 3.Geographical location

Many original apps and games support to get users' location through mobile hardware, and so does Egret.

You can get the equipments' current location by Egret's `Geolocation`class. It will distribute ` CHANGE ` events and pass the location changes to the callback function when you start to listen geolocation changes. Through ` GeolocationEvent ` types of callback parameters you can get the corresponding latitude, longitude, speed, altitude and other information through callback parameters of GeolocationEvent ` types.

### 3.1.Get geolocation information 

Sample codes are as follows:

```
/**
 * Get the location information and display it
 */
class GeolocationTest extends egret.DisplayObjectContainer {
    private label: egret.TextField;
    public  constructor() {
        super();
        //ldisplay info's label
        this.label = new egret.TextField();
        this.label.x = STAGEWIDTH / 2;
        this.addChild(this.label);
        this.label.size = 20;
        this.label.text = "Latitude and longitude information are not available yet";
        this.label.anchorOffsetX = this.label.width / 2;

        var gps = new egret.Geolocation();
        //Listen for events that vary in latitude and longitude
        gps.addEventListener(egret.Event.CHANGE,this.onGotLocation,this);
        //Start listening for changes
        gps.start();
    }
    private onGotLocation(e:egret.GeolocationEvent){
        this.label.text = "latitude: "+e.latitude.toFixed(4)+
            " altitude: "+e.altitude+
            "nlongitude:"+e.longitude.toFixed(4)
            +" speed: "+e.speed;
        this.label.anchorOffsetX = this.label.width / 2;
    }
}
```

Here to instantiate a ` Geolocation ` object, and add a listener to it. After `gps` execute `start()` method to monitor the location change. If there's a need to close monitor you can use its ` stop ` () method.
If you can get to the changes of loaction information, it will call `onGotLocation()`. The following properties are used to get the exact value of the location.

* latitude  
* longitude 
* altitude  
* speed     

It should be noticed that `altitude` and `speed` may be null.

### 3.2.Dealing with the failure to abtain the location

The user's permission is required to obtain the user's location information. And it will throw ` PERMISSION_DENIED ` event of ` GeolocationEvent `，if the user selects the do not share the current location information.

Add GPS monitor to our constructor above：
```
//Listen for user rejection events
gps.once(egret.GeolocationEvent.PERMISSION_DENIED,this.userDenied,this);
```
Add a handler in `GeolocationTest`, and send the message to the user：

```
private userDenied(e:egret.GeolocationEvent){
    this.label.text = "The user refused allowing others to access his location information, and failed to obtain the location information";
    this.label.anchorOffsetX = this.label.width / 2;
}
```

It will throw `UNAVAILABLE` event of ` GeolocationEvent ` if it failed with obtaining the location information for other reasons. Here to improve the procedures above, and add solutions when it cannot get information：

```
//listening failure event
gps.addEventListener(egret.GeolocationEvent.UNAVAILABLE,this.unAvailable,this);
```

Add a handler in `GeolocationTest`, and send the message to the user：

```
private unAvailable (e:egret.GeolocationEvent) {
    this.label.text = "failed to obtain the location information: " + e.errorMessage + "n"
        + "error type: " + e.errorType;
    this.label.anchorOffsetX = this.label.width / 2;
}
```

Here ` errorMessage ` represents it's failed to get the specific location information, and ` errorType ` represents the type of error.

