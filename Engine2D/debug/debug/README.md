
## 1.Compiling parameters with DEBUG
Developers often write codes that are desired to use only in development phase to perform data validation and output logs and more.

Egret provides the global variable  `DEBUG` to implement this function.

The following code verfies that  `value` is composed of 4 digits, and if not, system will prompt a specified error message.

```
	if (DEBUG) {
	    var rect = value.split(",");
	    if (rect.length != 4 || isNaN(parseInt(rect[0])) || isNaN(parseInt(rect[1])) ||
	        isNaN(parseInt(rect[2])) || isNaN(parseInt(rect[3]))) {
	        egret.$error(2016, this.currentClassName, toXMLString(node));
	    }
	}
```

In the process of release version making, Egret command line will remove the entire code block of `if(DEBUG){ ... }` to keep the simple of release version package.

Egret also provides another compilation parameter `RELEASE` that corresponds to `DEBUG`, which is used to write code that runs only in the release version.


## 2.Use built-in log output panel

On PC terminal, you can output log with the use of many methods provided by `console`, and then view them with the developer tools provided by the browser.

However, this method is limited on mobile terminal, because most mobile browsers don’t have a way to view logs.
So Egret integrates the function to output logs to the screen for users to have an easy mobile device debugging experience.


![Display log](p1.png)

There are the following code blocks in the index.html file:

```
    <div style="margin: auto;width: 100%;height: 100%;" class="egret-player"
         data-entry-class="Main"
         data-orientation="auto"
         data-scale-mode="showAll"
         data-frame-rate="30"
         data-content-width="640"
         data-content-height="1136"
         data-multi-fingered="2"
         data-show-fps="true" data-show-log="false"
         data-show-fps-style="x:0,y:0,size:12,textColor:0xffffff,bgAlpha:0.9"> 
     </div>
```

With data-show-log: set whether display the log on screen or not. true is display, false if not.

it's able to be directly called in codes:`egret.log(message?:any, ...optionalParams:any[])` to output log。

data-show-fps-style Able to set log’s location, font size and background color.

## 3.Display frame rate information

`data-show-fps="true/false"` set whether display frame rate information or not. When this value is `true`, Egret engine will display FPS and other performance indicators in the upper left corner of the stage.
		
* FPS:  60		- frame rate

* Draw: 13		- Average number called by draw method per frame
 
* Cost: 0,0		- 1) Time spent in Ticker and EnterFrame stage display; 2) time spent in drawing display objects (unit is ms) 

**Note: **Cost has three values in Egret engine 5.2 previous versions, which are: 1) time spent in Ticker and EnterFrame stage display; 2) time spent of all events processing each frame stage and matrix operations; 3) time spent in drawing display objects (unit is ms)


	