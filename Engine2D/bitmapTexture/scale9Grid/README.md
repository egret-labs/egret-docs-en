
Normally, for the aesthetic degree of the game screen, some rounded rectangles or irregular edges will be used. In the game, these graphics are often stretched, then the stretched graphics will be deformed. In order to make the edge not be deformed because of stretching, you can use the "Sudoku (Jiugongge)".

The following figure is a rounded rectangle

![](556564e1ddd8d.png)

The rounded rectangle is stretched in the transverse direction, and the stretching of the edge is changed as follows:

![](556564e1e524c.png)

The above effects do not meet the requirements, which will affect the artistic effect. Hope that no matter how the image is stretched, rounded corners will never be deformed, as shown below.

![](556564e1e5d41.png)

Jiugongge system can achieve the above effects.

![](556564e1e68d5.png)

In the above figure, the rounded rectangle is divided into nine zones with four dashed lines, of which four zones (zone is numbered 1, 3, 7, and 9 in the figure) contain four rounded corners of the rounded rectangle. When the image is stretched, the zones 1, 3, 7 and 9 won't be stretched, the zones 2 and 8 will be stretched only horizontally, and the zones 4 and 6 are stretched only in the longitudinal direction, and zone 5 is stretched both in longitudinal and horizontal directions.

Setting the attributes of the Jiugongge is the `scale9Grid` attribute in the `Bitmap` class.

The following is a complete example code. In this example, two `Bitmap` objects are placed and the two `Bitmap` objects will set the setting of width to two times of the original one. One of them adds Jiugongge data, while the other one does not add Jiugongge data.

```
class BitmapTest extends egret.DisplayObjectContainer{
    public constructor() {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    
    private onAddToStage(event:egret.Event) {
        RES.addEventListener(RES.ResourceEvent.GROUP_COMPLETE, this.onGroupComp, this);
        RES.loadConfig("resource/resource.json", "resource/");
        RES.loadGroup("preload");
    }
    private onGroupComp() {
        var img:egret.Bitmap = new egret.Bitmap();
        img.texture = RES.getRes("box");
        img.width *= 2;
        this.addChild(img);
        var img2:egret.Bitmap = new egret.Bitmap();
        img2.texture = RES.getRes("box");
        var rect:egret.Rectangle = new egret.Rectangle(30,31,40,41);
        img2.scale9Grid =rect;
        img2.width *= 2;
        img2.y = 150;
        this.addChild(img2);
    }
}
```

In the above code, an object of type `Rectangle` is created. The object is used to store Jiugongge data. Fill in four parameters when Initializing.

* 30: width of zone 1.

* 31: height value of zone 1

* 40: width value of zone 2

* 41: height value of zone 4

> Note: when setting the Jiugong width, please use integer as much as possible, otherwise "black line" may appear in some browsers. 

For more examples of Jiugongge, refer to [Teaching Examples] (http://developer.egret.com/cn/example/egret2d/index.html#050-bitmap-prac-9grid)

## Error handling

Under normal circumstances, the width and height of the Jiugongge zone must be less than the width and height of the image, the location of which is within the image. If the position or width and height of the set Jiugongge is abnormal,  the following error will be reported:

```
Warning #1018: The setting error of Jiugongge
```

Specifically, the correct Jiugongge is set to:
```
x + w <image width;
y + h <image height;
```
Where `x` and` y` are to set the position of the Jiugongge, while w and h are to set the width and height of the Jiugongge. Where x, y, w, h should be greater than or equal to 0.

> In the previous versions of Egret 3.0.3, x, y, w, h can not be set to 0.
