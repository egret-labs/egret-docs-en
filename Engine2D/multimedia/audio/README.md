
## 1. Create Sound
### 1.1. Install audio via Sound

* Create a `Sound` object through ```var sound:egret.Sound = new egret.Sound()```, then load through ```sound.load(url)```. `Sound` class supports two types of event types: `egret.Event.COMPLETE` audio is thrown when the load is finished; `egret.IOErrorEvent.IO_ERROR` audio is thrown when the load failed.

		var sound:egret.Sound = new egret.Sound();
        sound.addEventListener(egret.Event.COMPLETE, function loadOver(event:egret.Event) {	        sound.addEventListener(egret.Event.COMPLETE, function loadOver(event:egret.Event) {
			sound.play();
		}, this);
        sound.addEventListener(egret.IOErrorEvent.IO_ERROR, function loadError(event:egret.IOErrorEvent) {	        sound.addEventListener(egret.IOErrorEvent.IO_ERROR, function loadError(event:egret.IOErrorEvent) {
			console.log("loaded error!");
		}, this);
        sound.load("resource/sound/sound.mp3");	);


### 1.2. Install audio via URLLoader.

* The specific call is as follows.

		var loader:egret.URLLoader = new egret.URLLoader();
		loader.addEventListener(egret.Event.COMPLETE, function loadOver(event:egret.Event) {
			var sound:egret.Sound = loader.data;
			sound.play();
		}, this);
		loader.dataFormat = egret.URLLoaderDataFormat.SOUND;
		loader.load(new egret.URLRequest("resource/sound/sound.mp3"));

### 1.3. Install audio via res.

* The specific call is as follows.
 	 
		var sound:egret.Sound = RES.getRes("sound_mp3");
		sound.play();
        	        
## 2. Play Sound

### 2.1. Playback method

* Play audio with `play()` method, and there are 2 parameters.`startTime`: The position where the sound starts playing, by defaults it is 0.`loops`: The number of times the sound is played. When it is less than or equal to 0, it indicates infinite loop; when it is more than 0, it is played for the number of times according to the corresponding value.

* After running `play ()`, it returns a `SoundChannel` object, and the developer can manipulate `SoundChannel` directly, such as setting the volume.

The `egret.Event.SOUND_COMPLETE` event of the` SoundChannel` object is the event that has been played.

* The pause and replay functions are implemented based on the `position` attribute returned by` SoundChannel` and the `play ()` method of `Sound`.

* The `stop ()` method stops playing.

### 2.2.  Playback type

At present the engine provides four kinds of sound compatibility mode, namely, Audio, WebAudio, QQAudio (The sound solution provided by qzone), and NativeAudio (packaging program Audio)


* WebAudio: Browsers with IOS system version greater than or equal to 7. When the version is or later than Egret 3.2.0, by defuault Android also uses WebAudio. For app that doesn't support WebAudio, it will be automatically changed to Audio mode.

* QaAudio: The android models which is specified in the html page ""http://qzonestyle.gtimg.cn/qzone/phone/m/v4/widget/mobile/jsbridge.js"" (js api used by Qzone) and run in `qq space`.

* Audio: All other Web browsers or platforms except for those that use WebAudio and QQAudio.The possible problem is that there is a delay in the sound playback, and there is only one audio at the same time.

* NativeAudio: audio used by package program.


Set the playback type in the index.html template file under the project root directory: 

```
    /**
    * {
    * "renderMode":, //Engine rendering mode, "canvas" or "webgl"	webgl
: 0 // the type of audio used, 0: default, 1: qq audio, 2: web audio, 3: audio
: / /Under WebGL mode, whether to open anti-aliasing, true: open, false: off, it is false by default
: // whether the canvas is scaled based on devicePixelRatio
    * }
    **/
    egret.runEgret({renderMode:"webgl", audioType:0});	, audioType:0});
```

## 3. Audio example

A simple example code for playing audio is as follows:

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
        //Create a URLLoader object
        var loader:egret.URLLoader = new egret.URLLoader();
        //set the load mode to sound
        loader.dataFormat = egret.URLLoaderDataFormat.SOUND;
        //add the load to complete the listening
        loader.addEventListener(egret.Event.COMPLETE, this.onLoadComplete, this);
		//The audio resources are placed under the resource folder
        var url:string = "resource/soundtest.mp3";	;
        var request:egret.URLRequest = new egret.URLRequest(url);
        //start loading
        loader.load(request);
    }

    private onLoadComplete(event:egret.Event):void {
        var loader:egret.URLLoader = <egret.URLLoader>event.target;
        //Get the loaded Sound object
        var sound:egret.Sound = <egret.Sound>loader.data;
        this.sound = sound;
        //a simple play button
        var btn = new egret.Sprite();
        btn.graphics.beginFill(0x18f7ff);
        btn.graphics.drawRoundRect(0,0,80,40,5,5);
        btn.graphics.endFill();
        btn.touchEnabled = true;

        btn.anchorOffsetX = btn.width / 2;
        btn.x = this.stage.stageWidth / 2;
        btn.anchorOffsetY = btn.height / 2;
        btn.y = this.stage.stageHeight / 2;
        //Monitor the touch event of the button
        btn.addEventListener(egret.TouchEvent.TOUCH_TAP,this.onTouch,this);

        this.addChild(btn);
    }
    private sound:egret.Sound;
    private soundChannel:egret.SoundChannel;

    private onTouch(event:egret.Event){

        var sound = this.sound;
        var channel:egret.SoundChannel = this.soundChannel;
        if(channel){
            //Stop playing the audio by calling the soundChannel object
            console.log(channel);
            channel.stop();
            this.soundChannel = null;
            return;
        }
        //Use SoundChannel to play audio
        channel = sound.play(0,-1);
        //Egret 3.0.4 is added with the attribute of to getting the audio length.
        console.log(sound.length);
        channel.addEventListener(egret.Event.SOUND_COMPLETE, this.onSoundComplete, this);
        //Save the soundChannel object
        this.soundChannel = channel;
    }

    private onSoundComplete(event:egret.Event):void {
        console.log("onSoundComplete");	);
    }
}
```

First, use the `URLLoader` to load the audio, or you can load the audio with the above two other methods.Monitor the load completion event by monitoring the audio. When the load is completed, get the audio data and create a new `sound` object
Call the `play ()` method to play the audio. In this case, the unit of the start time is 0 seconds, loop.
Here ` play ` method returns a `SoundChannel` object. The volume is set by controlling the ``volume`` attribute  of `SoundChannel`, the volume ranging from 0 (quiet) to 1 (the maximum volume).The `position` attribute of the `SoundChannel` object can get the time of the current play, with unit of second.Note that the `position` attribute is a read-only one, so you can not set the time of the current play by setting `position`.
If you need to stop the sound, you can call the `stop ()` method of the `SoundChannel` object.


## 4. Precautions

* Please generate the format of the sound resource by strictly following this step, otherwise it will affect the compatibility.

1. Use the format factory.Select 44100Hz, 96kbps conversion.

2. If there is a problem, please turn it again.

3. If there is a problem, please cut the audio length and convert again.

4. If you have any question, please contact us at the forum [developer forum] (http://bbs.egret.com/portal.php) and provide the corresponding audio file.

>  If there is a problem, try to convert for  several times.
 	 
> For more professional conversion tools such as audition, it is found in the test that the converted file can not solve the playback problem in all the browsers, so it is not recommended.

> On iOS systems (all devices including IPAD), users need to wait for users' interaction operation before playing the media in the network environment where payment may be needed.To achieve the maximum compatibility in iOS system, please avoid using auto-play audio (load-on playback) and add the appropriate trigger conditions (such as the Play button).

> If you can not automatically play with the WebAudio mode, then there is no other way available for solving the problem of automatic playback.

* iOS game domain name must be under the domain name appointed by the Wanba, otherwise it can not use the js api (jsBridge) of the above-mentioned Qzone.

* Since some browsers do not support ""Play directly after Loading"", it is recommended that you preload the music files and call `sound.play ()` directly when you click on the event.

* For the audio that is not played with WebAudio method, it is likely that in the browser that only one kind of voice can be played at the same time (This is why qzone alone provides a sound solution).
