You can monitor the mouse events on a PC by using the [mouse support library] (https://github.com/egret-labs/egret-game-library/tree/master/mouse).

## 1. Introduce the mouse library

Introducing the mouse support library is the same as the introduction of other third-party libraries. First, [download] (https://github.com/egret-labs/egret-game-library/tree/master/mouse) library, then introduce the library in the egretProperties.json Introduce the library and compile the engine.Note that the location of the library should be placed outside the project.

```
{
    "name": "mouse",	,
    "path": "../libsrc"	../libsrc
}
```

After it is introduced into the project, the compiler engine can use the mouse library.

## 2. Support events

The following events are supported in the mouse support library.

| Name | description |
|---|---|
| MOUSE_MOVE | Called when the user moves the mouse.|
| MOUSE_OVER | Called when the mouse is within the object's area (not covered by other objects).|
| MOUSE_OUT | Called when the mouse is moved out of the object's area (not covered by other objects).|
| ROLL_OVER | Called when the mouse is moved into the area where the object is.|
| ROLL_OUT | Called when the mouse is moved out of the object's area.|

## 3. Usage

Mouse support needs to be enabled when mouse support library is used.

```
// Enable the mouse support for the stage
mouse.enable(this.stage);
```

Enable the stage's support for the mouse events by calling the enable method. You can monitor the mouse events after enabling support.The method of using mouse events is the same as that of other touch events. The basic call method is as follows:

```
mouse.enable(this.stage);
// Draw the outer container
this.outContainer = new egret.Sprite();
this.outContainer.name = "outContainer";	;
this.outContainer.graphics.beginFill(0x00ff00);
this.outContainer.graphics.drawRect(0, 0, 300, 300);
this.outContainer.graphics.endFill();
this.addChild(this.outContainer);
this.outContainer.x = (this.stage.stageWidth - this.outContainer.width) / 2;
this.outContainer.y = (this.stage.stageHeight - this.outContainer.height) / 2;
// Draw the inner layer display object
this.inShape = new egret.Sprite();
this.inShape.name = "inShape";	;
this.inShape.graphics.beginFill(0xff0000);
this.inShape.graphics.drawCircle(0, 0, 50);
this.inShape.graphics.endFill();
this.inShape.x = this.outContainer.width / 2;
this.inShape.y = this.outContainer.height / 2;
this.outContainer.addChild(this.inShape);
// Turn on the display object's touch
this.outContainer.touchEnabled = true;
this.inShape.touchEnabled = true;
// Monitor the MouseEvent of the outer container separately
this.outContainer.addEventListener(mouse.MouseEvent.ROLL_OVER, this.onRollOver, this);
this.outContainer.addEventListener(mouse.MouseEvent.ROLL_OUT, this.onRollOut, this);
this.outContainer.addEventListener(mouse.MouseEvent.MOUSE_OVER, this.onMouseOver, this);
this.outContainer.addEventListener(mouse.MouseEvent.MOUSE_OUT, this.onMouseOut, this);
//Display the MouseEvent of the displayed object by the monitored content
this.inShape.addEventListener(mouse.MouseEvent.ROLL_OVER, this.onRollOver2, this);
this.inShape.addEventListener(mouse.MouseEvent.ROLL_OUT, this.onRollOut2, this);
this.inShape.addEventListener(mouse.MouseEvent.MOUSE_OVER, this.onMouseOver2, this);
this.inShape.addEventListener(mouse.MouseEvent.MOUSE_OUT, this.onMouseOut2, this);
```

Where the callback function is as follows:

```
private onRollOver(e: egret.TouchEvent): void {
    console.log("roll over " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onRollOut(e: egret.TouchEvent): void {
    console.log("roll out " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onMouseOver(e: egret.TouchEvent): void {
    console.log("mouse over " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onMouseOut(e: egret.TouchEvent): void {
    console.log("mouse out " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onRollOver2(e: egret.TouchEvent): void {
    console.log("roll over2 " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onRollOut2(e: egret.TouchEvent): void {
    console.log("roll out2 " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onMouseOver2(e: egret.TouchEvent): void {
    console.log("mouse over2 " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}

private onMouseOut2(e: egret.TouchEvent): void {
    console.log("mouse out2 " + e.target.name + "  " + e.bubbles);	 + e.bubbles);
}
```

In the above code, two Sprites are drawn, one of which is used as the outer container, while the other as the internal display object. Compile, operate and observe the output results:

* MOUSE_OVER and ROLL_OVER will be thrown when the mouse is moved into the container and the inner display object.
* When the mouse is moved to the inner display object inside the container, the container will throw MOUSE_OUT rather than ROLL_OUT.
* When the mouse moves from the inner display object to the container, the container will throw MOUSE_OVER and the inner layer will throw ROLL_OUT and MOUSE_OUT.
* The container will throw ROLL_OUT when only the mouse is moved completely out of the container. 

Simple comparison shows the difference between MOUSE and ROLL: MOUSE_OVER and MOUSE_OUT are triggered on the visible area of the display object, while ROLL_OUT and ROLL_OUT are triggered on the display object as a whole.


### Set the mouse as hand shape

If you want to change the shape of the mouse as the shape of hand when the mouse is moved above the clickable area, you can set by `setButtonMode`.

```
// set the inner display object as hand-shape mouse
mouse.setButtonMode(this.inShape, true);
```

`setButtonMode` receives two parameters, the display object and whether to enable the hand-shape display.Once enabled, the mouse can be displayed as the shape of the hand when the mouse is moved above the display object.


### Monitor the mouse movement events

Monitoring the mouse movement events need to be enabled separately just by calling the `setMouseMoveEnabled ()` method.

```
//set to enable the mouse movement events
mouse.setMouseMoveEnabled(true);
```

Monitor this event after enabling the monitoring interface of the mouse movement event:

```
this.outContainer.addEventListener(mouse.MouseEvent.MOUSE_MOVE, function () { 
    console.log("mouse move"); 	); 
}, this);
```

> It should be noted that monitoring the mouse movement event will consume more performance.



