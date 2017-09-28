MovieClip (MC), also known as "movie clip", is an animated solution provided in Egret. Actually, the function of the MC is to play the sequence frame animation.

To achieve an animation effect, you can make the original animation an animation format that can be recognized by Egret .And then load these made resources and finally play it.

## 1. Make MovieClip animation resources
Egret offers three ways to create Egret animation resource files:

* Use TextureMerger to convert swf or gif files into Egret animation resource files.For the specific instructions, please refer to: [TextureMerger instructions] (http://bbs.egret.com/thread-918-1-1.html)

* Use DragonBones Pro to make frame animations.

* Egret provides a plug-in for Flash, which allows you to export animations in Flash as animation files that can be played by Egret.For plug-in installation and usage method, please refer to: [MovieClip Plug-in] (http://bbs.egret.com/thread-127-1-1.html)

## 2. Resource agreement

MovieClip requires a pair of json configuration files and a texture set of images.Such as `abc.json` and `abc.png`.

* The configuration file specifies the purpose of each field identifier,
* Texture set image is the image collection used by MovieClip.

### 2.1. Configuration parsing

~~~
{
	"mc": {
		"run": {
			"frameRate": 24,
			"events": [
				{
					"name": "@fall",
					"frame": 6
				}
			],
			"labels": [
                {	                {
                    "end": 8,	: 8,
                    "name": "start",	,
                    "frame": 2	: 2
                }	                }
            ],	            ],
			"frames": [
				{
					"res": "19236B52",
					"x": 6,
					"y": 13,
					"duration": 3
				}
			]
		}
	},
	"file": "abc.png",
	"res": {
		"19236B52": {
			"x": 111,
			"y": 1,
			"w": 108,
			"h": 131
		}
	}
}
~~~

* mc: Actions owned by MovieClip, such as the run here.
	* run: an action name that can have multiple ones.
		* frameRate: the frame rate of playback.
		* events: events triggered under a frame.
		* labels: labels that mark the frames of the current label.
		* frames: all frame data for the current action.
* file: Gallery name.
* res: texture set data.

### 2.2. Resource configuration

In the Egret's resource configuration file (By default it is `default.res.json`), there should be the following configuration:

~~~
"resources":	:
    [
         {"name":"abc.json","type":"json","url":"assets/abc.json"}	}
        ,{"name":"abc.png","type":"image","url":"assets/abc.png"}	}
        ......
    ]
~~~


## 3. Usage

### 3.1. Create

egret's MovieClip uses the factory pattern, with the MovieClip factory class as follows:
`MovieClipDataFactory`。

A MovieClip factory class corresponds to a MC resource collection.Such as resource files `abc.json` and `abc.png`.Then we can parse it into a MovieClip factory class in the program:

~~~
var data = RES.getRes("abc.json");	);
var txtr = RES.getRes("abc.png");	);
var mcFactory:egret.MovieClipDataFactory = new egret.MovieClipDataFactory( data, txtr );
~~~

### 3.2. Get action

Such as the above `run`. Then the method for parsing the MovieClip method in the program is:

~~~
var mc1:egret.MovieClip = new egret.MovieClip( mcFactory.generateMovieClipData( "run" ) );	 ) );
~~~

### 3.3. Playback

* Frame tag playback

 	If there is a frame label named "start" in MovieClip run, it will be played for three times here, with the code as follows:

~~~
this.addChild( mc1 );
mc1.gotoAndPlay( "start" ,3);	 ,3);
~~~

* Frame number playback
  For example, it will be played from the third frame, with the code as follows:

~~~
mc1.gotoAndPlay( 3 );
~~~

> Note: In order to avoid possible memory leak problems, MovieClip can not be played correctly until it has been added to the display list!

## 4. Events

### 4.1 Frame tag event

 The frame event tag can add monitoring to the animation to get this message

~~~
mc1.addEventListener(egret.MovieClipEvent.FRAME_LABEL,（e:egret.MovieClipEvent）=>{
	console.log(e.type,e.frameLabel, mc1.currentFrame);//frame_label @fall 6
},this);
~~~

### 4.2. Complete the event
For example, to play the animation for three times, the egret.Event.LOOP_COMPLETE event will be called for one time whenever the animation loop play is completed once. After the animation has been played for three times, the egret.Event.COMPLETE event will be called.

~~~
this.mc1.addEventListener(egret.Event.LOOP_COMPLETE, (e:egret.Event)=>{
	console.log(e.type);//Output for three times
}, this);
this.mc1.addEventListener(egret.Event.COMPLETE, (e:egret.Event)=>{
	console.log(e.type);//One time
}, this);
~~~
