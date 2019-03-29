`index.html` is the entry of the project file, the following is  `body` TAB in the default configuration, you can be modified according to the project requirements.

```
<div style="margin: auto;width: 100%;height: 100%;" class="egret-player"
         data-entry-class="Main"
         data-orientation="auto"
         data-scale-mode="showAll"
         data-frame-rate="30"
         data-content-width="640"
         data-content-height="1136"
         data-multi-fingered="2"
         data-show-fps="false" data-show-log="false"
         data-show-fps-style="x:0,y:0,size:12,textColor:0xffffff,bgAlpha:0.9">
    </div>
```

* data-entry-class：File class name.
* data-orientation：Rotation mode.
* data-scale-mode：Adaptive mode.
* data-frame-rate：Frame frequency.
* data-content-width：The width of the in-game stage.
* data-content-height：The height of the in-game stage.
* data-multi-fingered：Maximum quantity.
* data-show-fps：Whether to display FPS frame rate information.
* data-show-log：Display the output information of egret.log.
* data-show-fps-style：fps panel style. Supports 5 properties,，x:0, y:0, size:30, textColor:0xffffff, bgAlpha:0.9



In  `script`  tags, launch parameters of the project, as shown in the figure below

```
egret.runEgret({ renderMode: "webgl", audioType: 0, 
calculateCanvasScaleFactor:function(context) {
    var backingStore = context.backingStorePixelRatio ||
        context.webkitBackingStorePixelRatio ||
        context.mozBackingStorePixelRatio ||
        context.msBackingStorePixelRatio ||
        context.oBackingStorePixelRatio ||
        context.backingStorePixelRatio || 1;
    return (window.devicePixelRatio || 1) / backingStore;
}});
```

The parameter is an object, including the following three optional properties:

* "renderMode": engine renderMode, "canvas" or "webgl"
* "audioType": the use of audio type, 0, the default, 2: web audio, 3: audio  [the difference between the two, you can refer to the document](https://www.cnblogs.com/martinl/p/6005424.html)
* "calculateCanvasScaleFactor"：Screen physical pixel adaptation method, use the default

