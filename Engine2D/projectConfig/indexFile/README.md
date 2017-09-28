The entry file for the project is used to load the js file and set the configuration information.

    Native does not need to be configured separately, and the engine will automatically read various configuration information used by the project from the index.html.

## load the js file
The path of all the javascript files required for the project is stored in the manifest.json file of the project root directory.
The entry file loads the javascript file according to manifest.json.

	Here the script tags are automatically generated, do not modify.

### 1. Library file

 Included is a list of library files, including the Egret core library and other extension libraries.

### 2. Project code file

 Is the list of project code files.

## Run the configuration

* data-entry-class: file class name.
* data-orientation: rotation mode
* data-scale-mode: adaptation mode.
* data-frame-rate: frame frequency.
* data-content-width: the game stage width.
* data-content-height: the game stage height.
* data-show-pain-rect: whether to display the dirty rectangular area.
* data-multi-fingered: refers to the maximum number.
* data-show-fps: whether to display fps.
* data-show-log: whether to display the output information of egret.log.
* data-show-fps-style: fps panel style.Support five kinds of attributes, x: 0, y: 0, size: 30, textColor: 0xffffff, bgAlpha: 0.9

## Startup project
```egret.runEgret({ renderMode: "webgl", audioType: 0 })``` start the project.

The parameter is an object that includes the following four optional attributes:
* "renderMode": Engine rendering mode, "canvas" or "webgl" webgl
* "audioType": The type of the used video, 0: default, 2: web audio, 3: audio
* "antialias": Whether to open anti-aliasing in WebGL mode, true: on, false: off, the default is false
* "retina": Whether the zooming canvas is based on devicePixelRatio
