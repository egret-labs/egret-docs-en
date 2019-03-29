
## 1.Create Sound
### 1.1.Add Audio through Sound

* Create `Sound` object, through```var sound:egret.Sound = new egret.Sound()```,and load it through```sound.load(url)```, there're two types of events supported by `Sound`：`egret.Event.COMPLETE` thrown when the audio load is complete；`egret.IOErrorEvent.IO_ERROR` thrown when the audio load is failed.

		var sound:egret.Sound = new egret.Sound();
        sound.addEventListener(egret.Event.COMPLETE, function loadOver(event:egret.Event) {
			sound.play();
		}, this);
        sound.addEventListener(egret.IOErrorEvent.IO_ERROR, function loadError(event:egret.IOErrorEvent) {
			console.log("loaded error!");
		}, this);
        sound.load("resource/sound/sound.mp3");


### 1.2.Add Audio through URLLoader.

* The specific calls are as follows.

		var loader:egret.URLLoader = new egret.URLLoader();
		loader.addEventListener(egret.Event.COMPLETE, function loadOver(event:egret.Event) {
			var sound:egret.Sound = loader.data;
			sound.play();
		}, this);
		loader.dataFormat = egret.URLLoaderDataFormat.SOUND;
		loader.load(new egret.URLRequest("resource/sound/sound.mp3"));

### 1.3.Add Audio through res.

* The specific calls are as follows.
 	
		var sound:egret.Sound = RES.getRes("sound_mp3");
		sound.play();
        
## 2.Play Sound

### 2.1.Play method

* There're two parameters when playing sound by `play()` .`startTime`：where the sound starts to play，the default is 0.`loops`：the number of times the sound was played, if the value is less than or equal to 0, it will be played in an infinite loop; if it is greater than 0, it will be played several times according to the corresponding value.

* After running `play()` , it will return an object of `SoundChannel`, developers can manipulate `SoundChannel` directly，such as setting the volume,etc.

* The `egret.Event.SOUND_COMPLETE` event of object `SoundChannel`  stands for the play is complete.

* The pause and replay functions can be realized according to the `position` attribute returned by `SoundChannel` and the `play()` method of `Sound`.

* `stop()` The way to stop playing.

### 2.2.Play Type

At present, there're four sound compatibility modes are provided in the engine, namely Audio, WebAudio, QQAudio (sound solution provided by qzone), and NativeAudio (Audio packaging solution).


* WebAudio: all browsers with IOS higher than 7, Egret 3.2.0, and Android all use WebAudio by default. If the app doesn't support WebAudio, it will automatically change to Audio.

* QQAudio: specified  “ https://qzonestyle.gtimg.cn/qzone/hybrid/lib/jsbridge.js ” （js api used in Qzone）in the HTML page and android models run in ` Qzone ` .

* Audio: all Web browsers and platforms except the ones use WebAudio or QQAudio. One possible problem is that there is a delay in playing the sound, and only one audio can exist at a time.

* NativeAudio：audio used in packaging solutions.


Set the playback type in the index.html template file under the project root directory:

```
    /**
    * {
    * "renderMode":, //Engine's render mode，"canvas" or "webgl"
    * "audioType": 0 //audio type，0:default，1:qq audio，2:web audio，3:audio
    * "antialias": //Whether anti-aliasing is enabled in WebGL mode，true:enable，false:disable，the default is false
    * "retina": //Whether to scale the canvas based on devicePixelRatio
    * }
    **/
    egret.runEgret({renderMode:"webgl", audioType:0});
```

## 3.Audio sample

A simple example code to play the audio is shown below :

```
class SoundExample extends egret.DisplayObjectContainer {
    public constructor() {
        super();
        this.once(egret.Event.ADDED_TO_STAGE,this.onAddtoStage,this);
    }

    private onAddtoStage() {
        this.startLoad();
    }

    private startLoad():void {
        //Create URLLoader object
        var loader:egret.URLLoader = new egret.URLLoader();
        //Set the load mode to sound
        loader.dataFormat = egret.URLLoaderDataFormat.SOUND;
        //Add a load completion listener
        loader.addEventListener(egret.Event.COMPLETE, this.onLoadComplete, this);
		//Audio resources are placed under the resource folder
        var url:string = "resource/soundtest.mp3";
        var request:egret.URLRequest = new egret.URLRequest(url);
        //Start loading
        loader.load(request);
    }

    private onLoadComplete(event:egret.Event):void {
        var loader:egret.URLLoader = <egret.URLLoader>event.target;
        //Gets the loaded Sound object
        var sound:egret.Sound = <egret.Sound>loader.data;
        this.sound = sound;
        //A simple play button
        var btn = new egret.Sprite();
        btn.graphics.beginFill(0x18f7ff);
        btn.graphics.drawRoundRect(0,0,80,40,5,5);
        btn.graphics.endFill();
        btn.touchEnabled = true;

        btn.anchorOffsetX = btn.width / 2;
        btn.x = this.stage.stageWidth / 2;
        btn.anchorOffsetY = btn.height / 2;
        btn.y = this.stage.stageHeight / 2;
        //Listen for button touch events
        btn.addEventListener(egret.TouchEvent.TOUCH_TAP,this.onTouch,this);

        this.addChild(btn);
    }
    private sound:egret.Sound;
    private soundChannel:egret.SoundChannel;

    private onTouch(event:egret.Event){

        var sound = this.sound;
        var channel:egret.SoundChannel = this.soundChannel;
        if(channel){
            //Call the stop method of the soundChannel object to stop the audio playing
            console.log(channel);
            channel.stop();
            this.soundChannel = null;
            return;
        }
        //Play the audio using SoundChannel
        channel = sound.play(0,-1);
        //Add Egret 3.0.4 to get the audio length attribute.
        console.log(sound.length);
        channel.addEventListener(egret.Event.SOUND_COMPLETE, this.onSoundComplete, this);
        //Save soundChannel object
        this.soundChannel = channel;
    }

    private onSoundComplete(event:egret.Event):void {
        console.log("onSoundComplete");
    }
}
```

First use `URLLoader` to load audio，or you can also use the other two ways to load it. Listen to the audio loaded events, and to get and create `sound` object after loading is completed.
Call the method of `play()` to play audio, in this case, the unit of start time is 0 second, and loop playback. 
Here the `play` method will returns a `SoundChannel` object by controlling the `volume`attribute of `SoundChannel` to set the volume, the volume range from 0（quiet）to 1(maximum volume).
The`position` properties of `SoundChannel`object can get the current time, unit in seconds. It is important to notice that `position` is a read-only attribute, not by setting the `position`to change the current time.
If you need to stop the voices, you can call the `stop()` method of `SoundChannel` object.


## 4.Attentions

* Please follow these steps strictly for the format generation of sound resources, otherwise it will affect compatibility.

1. Use format factory. Select 44100Hz, 96kbps conversion.

2. If you have any questions, please turn again.

3. If there is still a problem, please cut the audio length again to convert.

4. If you still have any questions, please contact us [Developer BBS](http://bbs.egret.com/portal.php)，and provide the corresponding audio files。

> If you have any questions, please try to convert more times.
 
> For more professional conversion tools such as audition, I found in the test that the converted file could not solve the playing problems in all browsers, so we do not recommend you to use.

> In iOS (all devices, including the IPAD), users needs to wait for users interaction before playing media in paid network environment. In order to get the  maximum compatibility in iOS, please avoid using auto-play audio (which plays when the load is complete) and add appropriate trigger conditions (such as a play button).

> If WebAudio is not able to play automatically, there is no other way to deal with it.

* The js API (jsBridge) of Qzone mentioned above can only be used in the domain name specified by playbar for iOS games.

* Since some browsers do not support to play directly after loading, so it is recommended to preload the music file and call `sound.play()` directly when an event is clicked

* If you play audio in a non-webaudio mode, the browser probably can only play one sound at a time (that is why qzone provides a sound solution individually).
