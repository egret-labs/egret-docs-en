
## 1. Operation of the anchor
Each display object contains one anchor point, which is located in the upper-left corner of the display object by default.

When you set the coordinate position of a display object, the drawing position of the display object is changed with the anchor as a reference.At the same time, the anchor position relative to the display object position can also be changed.

### default anchor

```
class AnchorTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }

    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.beginFill( 0x00ff00 );
        shp.graphics.drawRect( 0, 0, 100, 100 );
        shp.graphics.endFill();
        shp.x = 100;
        shp.y = 100;
        this.addChild( shp );
    }
}
```

In the above code, a green square is drawn, and by default the anchor is at the upper left corner of the square. You can change the position of the square by setting the `x`,` y` attributes of `shp`.

The effect is as follows:

![](556535128a4a2.png)

### Modify anchor

The position of the anchor can be accessed and modified through the `anchorOffsetX` and `anchorOffsetY` attributes.

Modify the position of the above anchor, so that the anchor is at the upper left corner of the square, namely, the 50th pixel of the x-axis. The code is as follows:

```
shp.anchorOffsetX = 50;
```

Compile the project again and test, with the effect as follows:

![](556535128b8ba.png)

You can see that the green square position is still x: 100, y: 100.But in the actual effect, the position of the square is significantly different from that of the above image.This is because the position of the anchor is modified.

## 2. Position and pan

### location
The position of object can be accessed and modified through the x and y attributes.

``` 
container.x = 17;
container.y = 212;
```

The display object positioning system treats the stage as a Cartesian coordinate system (a common grid system with horizontal x-axis and vertical y-axis).The origin of the coordinate system (the 0, 0 coordinate where the x and y axes intersect) is located in the upper left corner of the stage.Starting from the origin, the value of the x-axis is positive to the right, negative to the left, and the value of the y-axis is positive downward and negative upward (as opposed to a typical graphics system).For example, the object container can be moved to x-axis coordinates 17 (17 pixels to the right) and y-axis coordinates 212 (212 pixels down) through the previous line of code.

When the display object is created by default, the x and y attributes are set to 0, and the object is in the upper-left corner of its parent container.

### Local coordinates and stage coordinates

The x and y attributes always refer to the position of the display object relative to the (0,0) coordinates of the parent display axis.Thus, for a Shape instance (such as a circle) contained in a DisplayObjectContainer instance, if you set the x and y attributes of the Shape object to 0, the circle is placed in the upper-left corner of the DisplayObjectContainer, but the position is not necessarily the upper-left corner of the stage.To determine the position of an object relative to the global stage coordinates, you can use the globalToLocal () method of any display object to convert the coordinates from the global (relative to stage) coordinates to the local (relative to the display object container) coordinates, as follows:
 	 
```
//Create an empty DisplayObjectContainer, change its x and y coordinates to
var container: egret.DisplayObjectContainer = new egret.DisplayObjectContainer();
container.x = 200;
container.y = 200;
this.addChild(container);

//draw a red circle and add it to the container
var circle: egret.Shape = new egret.Shape();
circle.graphics.beginFill(0xff0000);
circle.graphics.drawCircle(25,25,25);
circle.graphics.endFill();
container.addChild(circle);

//Add a clicking event to the circle
circle.touchEnabled = true;
circle.addEventListener(egret.TouchEvent.TOUCH_TAP,onClick,this);

function onClick():void{
    // Converts the coordinates (0,0) in the upper left corner of the stage to the coordinates inside the container
    var targetPoint: egret.Point = container.globalToLocal(0,0);
    //reposition the circle, so that you can see the circle is moved to the upper left corner of the screen
    circle.x = targetPoint.x;
    circle.y = targetPoint.y;
    }
}
```

Likewise, you can also use the localToGlobal () method of the DisplayObject class to convert local coordinates to the stage coordinates.

### Panning

Move the display object by touch, with the sample code as follows:

When the finger is pressed on the screen to monitor the TOUCH_MOVE event, the `onMove ()` function is called each time the finger moves, causing the dragged object to jump to the x, y coordinates where the finger is located.When the finger leaves the screen to cancel the monitoring, the object stops following.

```
//set two offsets
var offsetX:number;
var offsetY:number;

// Draw a red circle
var circle: egret.Shape = new egret.Shape();
circle.graphics.beginFill(0xff0000);
circle.graphics.drawCircle(25,25,25);
circle.graphics.endFill();
this.addChild(circle);

//press finger on the screen to trigger the startMove method
circle.touchEnabled = true;
circle.addEventListener(egret.TouchEvent.TOUCH_BEGIN,startMove,this);

//when the finger leaves the screen, the stopMove method is triggered
circle.addEventListener(egret.TouchEvent.TOUCH_END,stopMove,this);

function startMove(e:egret.TouchEvent):void{
  //Calculate the distance between the finger and the circle
  offsetX = e.stageX - circle.x;
  offsetY = e.stageY - circle.y;
  //when the finger moves on the screen, the onMove method will be triggered
  this.stage.addEventListener(egret.TouchEvent.TOUCH_MOVE,onMove,this);
}

function stopMove(e:egret.TouchEvent) {console.log(22);
   //when the finger leaves the screen, the monitoring by moving finger is removed
   this.stage.removeEventListener(egret.TouchEvent.TOUCH_MOVE,onMove,this);
}
function onMove(e:egret.TouchEvent):void{
   //calculate the coordinates of the current object by calculating the position of the finger on the screen, so as to achieve the effect of moving with the finger
   circle.x = e.stageX - offsetX;
   circle.y = e.stageY - offsetY;
}
```
 	 
## 3. Size and zoom

There are two ways to measure and manipulate the size of the display object: the size attribute (width and height) or the zoom attribute (scaleX and scaleY).

### size
The size attributes `width` and `height` are initially set to the size of the object in pixels.You can determine the size of the display object by reading the value of these attributes, or you can change the size of the object by specifying a new value, which is as follows:

```  TypeScript
//set the size of the object
mySprite.width = 50;
mySprite.height = 100;
```
Changing the height or width of the display object will cause the object to be scaled.

### Zoom

By scaling the attributes `scaleX` and `scaleY`, you can change the size of the display object, as shown in the following code:

```
//set the size of the object
mySprite.scaleX = 2;
mySprite.scaleY = 2;
```

The width and height of the display object are enlarged 2 times at the same time.The zoom is made relative to the anchor of the display object.

## 4. Rotate

Use the `rotation` attribute to rotate the display object, and set it to a number (in degrees), which indicates the amount of rotation applied to the object, with positive being clockwise and negative being counterclockwise.Rotation is performed relative to the anchor of the display object.

The following code causes `mySprit` to rotate 45 ° clockwise with anchor as the center of a circle.

```
//Rotate the object by 45 degrees (1/8 of the whole week)
mySprite.rotation = 45;
```

## 5. Beveling

The beveling is a parallel matrix deformation of the image in 2D space.

The beveling can be controlled from both directions, and the beveling in the X direction will cause the bottom edge of the rectangle to shift accordingly in the X direction.

![skewX_compare][]    

As shown in the figure above, it is the result of the X-direction beveling 10 of the Egret bird.The left is the original image that is not deformed, and the right is the deformed image.  

```
//set the object's X-direction beveling
mySprite.skewX = 10;
```

Similarly, the beveling in the Y direction will cause the right side of the rectangle to shift accordingly in the Y direction.

![skewY_compare][]    

As shown in the figure above, it is the result of the Y-direction beveling 10 of the Egret bird.   

[skewX_compare]: skewX_compare.png
[skewY_compare]: skewY_compare.png

```
//set the object's Y-direction beveling
mySprite.skewY = 10;
```

In the appropriate animation, the presentation occasions use beveling deformation, so that you can achieve flexible and interesting effects without increasing image resources.   
