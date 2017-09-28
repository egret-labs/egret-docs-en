Egret package `Graphics` class to achieve vector graphics function. You can draw a rectangle, round, straight, curve, arc and so on. Next we will introduce the basic usage of vector graphics and a number of advanced usage.

## 1. Draw a rectangle

The drawing method encapsulated in the `Graphics` class cannot be used directly and needs to be used in the display object. Some display objects (such as `Shape` and` Sprite`) already contain drawing methods, so you can call these methods directly in the display object for drawing.

Taking `Shape` as an example, the following codes draw a rectangle:

```
class GraphicsTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.beginFill( 0xff0000, 1);
        shp.graphics.drawRect( 0, 0, 100, 200 );
        shp.graphics.endFill();
        this.addChild( shp );
    }
}
```

Run after compilation, with the effect shown as below:

![](5565675e01970.png)

The following three lines are the core drawing codes of the codes:

```
shp.graphics.beginFill( 0xff0000, 1); 
shp.graphics.drawRect( 0, 0, 100, 200 ); 
shp.graphics.endFill();
```

Accessing the `graphics` attribute of `shp` will return a `Graphics`, the drawing method of which can be operated for implementing the drawing.

Call the `beginFill ()` method to set the filling color of the rectangle, where the filling color is set to red (color value 0xff0000), while setting `alpha` to 1 to indicate that it is completely opaque.

Call the `drawRect ()` method to set the position and size of the rectangle. The former two parameters are the X and Y coordinates of the upper left corner of the rectangle (relative to the anchor point of `shp`). The latter two parameters are respectively the width and height of the rectangular. Here we draw a 100*200 rectangle at (0, 0) point.

Call the 'endFill () `method to end the current drawing operation.

To add a stroke to a rectangle, set the style of the line with the `lineStyle ()` method.

The first parameter of the method is the line width of the stroke, and the second parameter is the color of the stroke.

Add a line to the drawing codes:

```
shp.graphics.lineStyle( 10, 0x00ff00 );
```

The modified code is as follows:

```
class GraphicsTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.x = 20;
        shp.y = 20;
        shp.graphics.lineStyle( 10, 0x00ff00 );
        shp.graphics.beginFill( 0xff0000, 1);
        shp.graphics.drawRect( 0, 0, 100, 200 );
        shp.graphics.endFill();
        this.addChild( shp );
    }
}
```

Compile and run, with the effect shown as below:

![](5565675e02ce3.png)

## 2. Draw a circle

The method of drawing a circle is similar to drawing a rectangle. You just need to change the `drawRect ()` method to the `drawCircle ()` method.

```
drawCircle( x:number, y:number, radius:number): void
```

The `drawCircle ()` method accepts three parameters, of which the first is the X-axis coordinate of the center, the second is the Y-axis coordinate of the center, and the third is the radius.

> Note: The X and Y axis positions of the center are calculated relative to the anchor point of the `Shape` object.

The following code example draws a circle with a radius of 50 pixels:

```
class GraphicsTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.x = 100;
        shp.y = 100;
        shp.graphics.lineStyle( 10, 0x00ff00 );
        shp.graphics.beginFill( 0xff0000, 1);
        shp.graphics.drawCircle( 0, 0, 50 );
        shp.graphics.endFill();
        this.addChild( shp );
    }
}
```

Compile and run, with the effect shown as below:

![](5661535675def.png)

## 3. Draw a straight line

Two methods are needed when drawing a line with Graphics: `moveTo ()` and `lineTo ()`, and their input parameters are a pair of coordinate values. `moveTo ()` is responsible for drawing the starting point of the line, and `lineTo ()` is responsible for drawing the end of the line.

```
moveTo( x:number, y:number): void
lineTo( x:number, y:number): void
```

Before drawing a line, you need to first create a line style, and set the `lineStyle ()` method:

```
shp.graphics.lineStyle( 2, 0x00ff00 );
```

Then use `moveTo ()` to set the starting point of the line, and use `lineTo ()` to set the end of the line. The complete code is as follows:

```
class GraphicsTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.lineStyle( 2, 0x00ff00 );
        shp.graphics.moveTo( 10,10 );
        shp.graphics.lineTo( 100, 20 );
        shp.graphics.endFill();
        this.addChild( shp );
    }
}
```

Run after compilation, with the effect shown as below:

![](566153894306a.png)

You can also draw a number of end-to-end straight lines, forming a polyline, with the code as follows:

```
var shp:egret.Shape = new egret.Shape();

shp.graphics.lineStyle( 2, 0x00ff00 );

shp.graphics.moveTo( 68, 84 );

shp.graphics.lineTo( 167, 76 );

shp.graphics.lineTo( 221, 118 );

shp.graphics.lineTo( 290, 162 );

shp.graphics.lineTo( 297, 228 );

shp.graphics.lineTo( 412, 250 );

shp.graphics.lineTo( 443, 174 );

shp.graphics.endFill();

this.addChild( shp );
```

> When you draw a polyline, you can use the `lineTo ()` method continuously, without the need to use the `moveTo ()` method for multiple times.

Run after compilation, with the effect shown as below:

![](5661538977888.png)

## 4. Draw the curve
The curve provided in Egret is the "second Bezier curve". The following figure is the structure of the "second Bezier curve", where P0 is the starting point, P1 is the control point and P2 is the end point.

![](566153b5385e7.png)

When drawing a curve, please use the `curveTo ()` method in `Graphics`.

```
curveTo( x1:number, y1:number, x2:number, y2:number ): void
```

The `curveTo ()` method requires four parameters, of which the former two ones are the position of the control point (P1), and the latter two ones are the position of the end point (P2).

When you execute a drawing, first use the `moveTo ()` method to specify the starting point of the curve, and then use `curveTo ()` to specify the control point and end point of the curve. When the program is drawing, the drawing process is as follows:

![](566153b54d721.gif)

Sample code:

```
class GraphicsTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.lineStyle( 2, 0x00ff00 );
        shp.graphics.moveTo( 50, 50);
        shp.graphics.curveTo( 100,100, 200,50);
        shp.graphics.endFill();
        this.addChild( shp );
    }
}
```

Run after compilation, with the effect shown as below:

![](566153b573f6a.png)

## 5. Draw the arc

Draw a closed arc using the `drawArc ()` method in `Graphics`.

```
drawArc( x:number, y:number, radius:number, startAngle:number, endAngle:number, anticlockwise:boolean ):void
```

The first two parameters are the center of the arc path, and `radius` is the radius of the arc. `startAngle` is the angle of the starting point of the arc, which is calculated from the x-axis direction and take radians as the unit. `endAngle` is the angle of the arc end point, `anticlockwise` controls the drawing direction. If it is true, draw the arc counterclockwise, otherwise please do so clockwise.

The following example draws an arc from 0 to π:

```
class GraphicsTest extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event)
    {
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.beginFill( 0x1122cc );
        shp.graphics.drawArc(200,200,100,0,Math.PI,true);
        shp.graphics.endFill();
        this.addChild( shp );
    }
}
```

Compile and run, with the effect shown as below:

![](55fa85513f04e.png)

Where endAngle uses `Math.PI` to represent radians π, which can be queried in the math-related API.

http://developer.egret.com/cn/apidoc/index/name/global.Math

## 6. Draw advanced arc usage

### 6.1. Draw the arc

~~~
var shape:egret.Shape = new egret.Shape();
shape.graphics.lineStyle(2, 0xffff00);
shape.graphics.drawArc(50, 50, 50, 0, Math.PI / 180 * 30, false);
shape.graphics.endFill();
~~~

![](569f036c09b4d.png)

### 6.2. Draw the arch

~~~
var shape:egret.Shape = new egret.Shape();
shape.graphics.beginFill(0xff0000);
shape.graphics.drawArc(50, 50, 50, 0, Math.PI / 180 * 60, false);
shape.graphics.endFill();
~~~

![](569f036c2577d.png)

> The difference between the arch and the arc is that the drawing arch needs to fill the pattern and the arc does not need to fill the pattern.

### 6.3. Draw the sector

In fact, the sector is the closed area after the center of the circle connects with the two ends of the arc.

~~~
var r:number = 50;
var shape:egret.Shape = new egret.Shape();
shape.graphics.beginFill(0xff0000);
shape.graphics.moveTo(r, r);//The drawing point moves (r, r) point
shape.graphics.lineTo(r * 2, r);//draw lines to the starting point of the arc点
shape.graphics.drawArc(50, 50, 50, 0, 260 * Math.PI / 180, false);//draw arch clockwise from the starting point to the end point
shape.graphics.lineTo(r, r);//draw lines from the finish line to the circle. The following is fored in this fan-shaped closed area 
shape.graphics.endFill();
~~~

![](569f036be6477.png)

### 6.4. Draw a curved progress bar

~~~
private getArcProgress():egret.Shape {
    var shape:egret.Shape = new egret.Shape();
    var angle:number = 0;
    egret.startTick(function (timeStamp:number):boolean {
        angle += 1;
        changeGraphics(angle);
        angle = angle % 360;

        return true;
    }, this);

    function changeGraphics(angle) {
        shape.graphics.clear();

        shape.graphics.lineStyle(2, 0x0000ff, 1);
        shape.graphics.drawArc(50, 50, 50, 0, angle * Math.PI / 180, false);
        shape.graphics.endFill();
    }
}
~~~

For the use of `egret.startTick` in the code, refer to [Timer Timer] ../../timeControl/timer)

### 6.5. Draw fan-shaped progress bar

~~~
private getSectorProgress():egret.Shape {
    var shape:egret.Shape = new egret.Shape();

    var angle:number = 0;
    egret.startTick(function (timeStamp:number):boolean {
        angle += 1;
        changeGraphics(angle);
        angle = angle % 360;

        return true;
    }, this);
    
    return shape;

    function changeGraphics(angle) {
        shape.graphics.clear();

        shape.graphics.beginFill(0xff0000);
        shape.graphics.moveTo(50, 50);
        shape.graphics.lineTo(100, 50);
        shape.graphics.drawArc(50, 50, 50, 0, angle * Math.PI / 180, false);
        shape.graphics.lineTo(50, 50);
        shape.graphics.endFill();
    }
}
~~~

### 6.6. Draw irregular bar progress bar

The following is an example of simulating the progress of the border by combining the mask (`mask`) and the fan-shaped progress bar. For the specific usage of `mask`, refer to [mask] (../../mask/rectangleMask)

* * First, provide a fully enclosed graphic with only borders. Such as

![](569f036c525df.png)

* * Use the fan-shaped progress bar described above and ensure that the area of the circle defined by the sector can completely cover the border map. To align the center of the sector with the center of the frame.

* Set the `mask' of the border to the fan-shaped progress bar, thus completing a simple border progress bar. You can complete the progress bar suitable for the project by modifying the masked graphics. For example, graphics is not a border, but a gray-box fill map.

![](569f036bbe628.png)

* Code:

~~~
private drawBorderProgress():egret.DisplayObjectContainer {
    var container:egret.DisplayObjectContainer = new egret.DisplayObjectContainer();
    var w:number = 100;
    var h:number = 100;
    var r:number = Math.max(w, h) / 2 * 1.5;
    var bitmap = new egret.Bitmap(RES.getRes(key));
    container.addChild(bitmap);
    bitmap.width = w;
    bitmap.height = h;

    var shape:egret.Shape = new egret.Shape();
    shape.x = bitmap.width / 2;
    shape.y = bitmap.height / 2;

    bitmap.mask = shape;
    container.addChild(shape);

    var angle = 0;
    egret.startTick(function (timeStamp:number):boolean {
        angle += 1;
        changeGraphics(angle);
        angle = angle % 360;

        return true;
    }, this);

    return container;

    function changeGraphics(angle) {
        shape.graphics.clear();

        shape.graphics.beginFill(0x00ffff, 1);
        shape.graphics.lineTo(r, 0);
        shape.graphics.drawArc(0, 0, r, 0, angle * Math.PI / 180, true);
        shape.graphics.lineTo(0, 0);
        shape.graphics.endFill();
    }
}
~~~

* Renderings

![](569f036ba015a.png)   ![](569f036bbe628.png)


> Since `mask` heavily consumes CPU, it is suggested that you'd better minimize the use of continuous modification of `mask` when drawing.

## 7. Draw multiple shapes

The following code draws four small cells in a `Shape` object, next to each other, and red and blue.

```
this.graphics.beginFill( 0x0000ff );
this.graphics.drawRect( 0, 0, 50,50 );
this.graphics.endFill();

this.graphics.beginFill( 0x0000ff );
this.graphics.drawRect( 50, 50, 50, 50);
this.graphics.endFill();

this.graphics.beginFill( 0xff0000 );
this.graphics.drawRect( 50, 0, 50,50 );
this.graphics.endFill();

this.graphics.beginFill( 0xff0000 );
this.graphics.drawRect( 0, 50, 50,50 );
this.graphics.endFill();
```

Put the `Shape` object into the display list, compile and run, thus getting the effect as shown below:

![](566153e55d510.png)

> Note: Multiple shapes are drawn, independent of each other. Each time when you draw and fill, you must end with `endFill ()` before starting the next drawing.


## 8. Empty the drawing

The operation of emptying the drawing is to empty all the images that have been drawn, by executing the `clear ()` method in `Graphics`, with codes as follows:

```
shp.graphics.clear();
```
