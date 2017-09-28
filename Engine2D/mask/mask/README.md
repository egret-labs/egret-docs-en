
The role of the mask is to specify the visible area of a display object, with all display objects capable of masking function.

## 1. Rectangular mask

The rectangular mask means that the visible area of the display object is a square display area rather than an irregular display area.

Usage: Assign a rectangle object to the `mask` attribute of the display object.

~~~
shp.mask = new egret.Rectangle(20,20,30,50); 
~~~

> If `rect` changes, you need to reassign `rect` to `shp.mask`.

The following example draws two `Shape` objects, one `Shape` of which uses rectangular mask and another `Shape` of which is used as a reference. The code is as follows:

~~~
class Test extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }

    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.beginFill( 0xff0000 );
        shp.graphics.drawRect( 0,0,100,100);
        shp.graphics.endFill();
        this.addChild( shp );

        var shp2:egret.Shape = new egret.Shape();
        shp2.graphics.beginFill( 0x00ff00 );
        shp2.graphics.drawCircle( 0,0, 20);
        shp2.graphics.endFill();
        this.addChild( shp2 );
        shp2.x = 20;
        shp2.y = 20;
    }
}
~~~

Compile and run, and the effect is as follows:

![image](55653415102ac.png)

Now add a mask to `shp`, and the specific code is as follows:

~~~
var rect:egret.Rectangle = new egret.Rectangle(20,20,30,50);  
shp.mask = rect;
~~~


Compile and run, and the effect is as follows:

![image](5565341511ede.png)

It can be seen that only the image of the (20, 20, 30, 50) part is displayed after mask is added to the red square. The green circle to which no mask is added still remains complete


# 2. Display the object mask

The display object mask, namely, the visible area of the display object is determined by another display object, capable of achieving an irregular mask.

Usage: Set the `mask` attribute of the masked display object is set to the masked object:

```
//Set maskSprite as the mask of mySprite
mySprite.mask = maskSprite;
```
The display area of the masked display object is within the entire opaque area of the display object used as the mask. For example, the following code creates a `Shape` instance containing a red square of 100 x 100 pixels and a `Sprite` instance containing a blue circle with a radius of 25 pixels, which is set to a square mask. The square display area is the part covered by the opaque area of the circle.

```
//Draw a red square
 var square:egret.Shape = new egret.Shape();
 square.graphics.beginFill(0xff0000);
 square.graphics.drawRect(0,0,100,100);
 square.graphics.endFill();
 this.addChild(square);

//Draw a blue circle
var circle:egret.Shape = new egret.Shape();
circle.graphics.beginFill(0x0000ff);
circle.graphics.drawCircle(25,25,25);
circle.graphics.endFill();
this.addChild(circle);

square.mask = circle;
```
The final effect is shown as below

![](55a32cdb75779.png)

The display object used as a mask can be animated and dynamically resized. The masked display object does not necessarily need to be added to the display list. However, if you want to zoom in/out the masked object while zooming in/out the stage, or if you want to support user interaction with the masked object (such as resizing), you must add the masked object to the display list.

You can delete the mask by setting the `mask` attribute to` null`:

```
mySprite.mask = null;
```
> You can not use one masked object to mask another masked object.

> Display object, as a mask, needn't repeat the assignment of `mask`, but `mask` must be an element in the display list.

