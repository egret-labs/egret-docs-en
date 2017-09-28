Easing animation is a common part of the game.For example, interface pop-up, and the effects of props flying in and out. The Tween easing animation class in Egret provides related functionality.

## 1. Make sure the project supports Tween

In the Egret project, modify the `modules` in egretProperties.json and add the `tween` module:
```
 {
     "name": "tween"
 }
 ```
Perform the engine compilation for one time in the project's directory:

```
egret build -e
```

## 2. Basic usage of easing animation

`Tween` encapsulates the most commonly used easing animation features, including animation time settings, easing animation control, and easing effect control, etc.Here is an example of a easing animation.

In this example, draw a 100 * 100 square and move it from the position of 50 x-axis to the position of 150 x-axis, which will take the time of 1s.

![](568b43fa06115.gif)

The specific code is as follows:

```
/// code segment A
class TweenTest extends egret.DisplayObjectContainer{
    public constructor(){
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private onAddToStage(event:egret.Event){
        var shp:egret.Shape = new egret.Shape();
        shp.graphics.beginFill( 0x00ff00 );
        shp.graphics.drawRect( 0, 0, 100, 100 );
        shp.graphics.endFill();
        shp.x = 50;
        this.addChild( shp );
        var tw = egret.Tween.get( shp );
        tw.to( {x:150}, 1000 );
    }
}
```

As shown in the code, the easing object is obtained with `Tween.get ()`, which requires to pass the target object for easing, that is the `shp` in the example. Then give the specific parameter that needs to be set to easing with the `to ()` method.The first parameter of `to ()` is used to set the easing attribute and the target value: the attribute in the example is x, the target value is 150, which slowly moves the shp from the current x coordinate position to the x coordinate 150; the second parameter of `to()` is the length of easing time (in milliseconds), where the length of the easing is 1000 milliseconds, or 1 second.

## 3. The basic control parameters of the easing object 

In the definition of easing, you can also pass some of the attribute parameters for further customization.

The second parameter of `Tween.get ()`  is optional. It is an object parameter that supports two attributes, which is explained respectively:

* loop is a Boolean value that specifies whether to loop the easing definition.true for the loop, and false for no loop. By default it is not loop (false).

* useTicks is a Boolean value that specifies whether to use frame synchronization.There are two ways to calculate the easing of the easing attribute. One is to consider the running time of each frame and the impact of the length of each frame on  easing, which will automatically calculate the time difference to determine the current frame interpolation; the other is that the time for setting each frame is constant, which will cause unstable animation process when the execution time of each frame changes dramatically. By default, the value considers the time difference (false).

For example, to add loop control to segment A of the code, just change `Tween.get ()`:

```
var tw = egret.Tween.get( shp, { loop:true} );
```

## 4. Ease the object's easing change event

In the implementation of `Tween`, maybe some changes need to be made to the logic in real time.Tracking this process can also be achieved by adding the definition of the change event handler in the second parameter of the `Tween.get ()`.

For example, when a prey in the game is in the Tween movement process, the hunter must target his gun towards the prey in a real-time manner. Then you need to calculate the changing process of Tween, so as to amend the angle of the hunter's muzzle.

Taking a simple example, log out the changed coordinates:

```
/// code segment B
var obj = { x:0 };

var funcChange = function():void{
    console.log( this.x );
}

egret.Tween.get( obj, { onChange:funcChange, onChangeObj:obj } )
    .to( {x:600}, 1000 , egret.Ease.backInOut );
```

## 5. Parameter settings of the easing process

The third parameter of the `to ()` method towards the control easing process also needs to be specifically explained.This parameter specifies the easing function, namely, the changing manner of attribute in the entire animation process is uniform, or fast at first and slow later, or slow at first and fast later, etc.This can be set by the function constants provided in the existing Ease. 

For example, in the code segment B, the `Ease.backInOut` easing equation is used. The attribute change curve of the easing equation has a short reverse motion in the beginning and end stages of the easing. For the specific changing manner of each easing function, visual effect can be seen from the [Tween Effects of EDN Center] (http://edn.egret.com/cn/article/index/id/53).


## 6. Other methods of easing the object

For the control of easing, you can set a number of other methods.There are the following two main methods:

* `call ()` At the end of certain easing process, you can use `call ()` to generate a callback, passing the callback function directly as a parameter to `call ()`.

* `wait ()` is used to set the waiting time in milliseconds for multiple continuous settings for easing.

## 7. Continuous setting of multiple easing processes

In addition to completing a single easing animation, the easing objects can also continuously implement several easing by continuously calling the easing process method.Here an animation is designed for showing how a small box moves in a square orbit, which will indicate it is at which corner the callback event is generated and will stay in the corner for a while. The following is a complete code:

```
/// code segment C.
var shp:egret.Shape = new egret.Shape();
shp.graphics.beginFill( 0x00ff00 );
shp.graphics.drawRect( 0, 0, 100, 100 );
shp.graphics.endFill();
shp.x = 50;
shp.y = 50;
this.addChild( shp );
var tw = egret.Tween.get( shp, { loop:true} );
tw.to( {x:250}, 500 ).call( function(){ console.log( "top right corner" ) } ).wait( 100 )	 ) } ).wait( 100 )
    .to( {y:250}, 500 ).call( function(){ console.log( "bottom right corner" ) } ).wait( 100 )	 ) } ).wait( 100 )
    .to( {x:50}, 500 ).call( function(){ console.log( "lower left quarter" ) } ).wait( 100 )	 ) } ).wait( 100 )
    .to( {y:50}, 500 ).call( function(){ console.log( "top left corner" ) } ).wait( 100 );	 ) } ).wait( 100 );
```
