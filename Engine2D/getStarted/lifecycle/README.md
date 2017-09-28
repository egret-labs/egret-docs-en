In the game, the user can switch between the foreground and background of the application.When the user enters the background, turn off the game logic, rendering logic and background music, thus ensuring a better user experience.

### Egret Engine v2.0 + API

In the Egret Engine 2.0+ version, the lifecycle control is implemented by monitoring the ```egret.Event.ACTIVATE``` and ```egret.Event.DEACTIVATE``` events of the ```stage``` object

```typescript
stage.addEventListener(egret.Event.ACTIVATE,()=>{
    console.log("app enters the foreground");
},this);
stage.addEventListener(egret.Event.DEACTIVATE,()=>{
    console.log("app enters the background");
},this);
```

The shortcomings of the above method are:

1. The object's ""lifecycle"" behavior is coupled with the ```stage``` object."
2. Because the operating environment of some HTML5 games  (such as mobile QQ) set a unique API rather than HTML5 standard API, it is difficult for developers to customize the expansion at the bottom of the Egret Engine.

### Egrets engine v4.1 + API

Egret Engine version 4.1 introduces lifecycle manager: ```egret.lifecycle```.The code example is as follows:

```typescript
egret.lifecycle.onPause = ()=> {
    console.log("app enters the background");
    egret.ticker.pause(); // Close the rendering and heartbeat
}
egret.lifecycle.onResume = ()=> {
    console.log("app enters the foreground");
    egret.ticker.resume(); // Open the rendering and heartbeat
}
```

For the operating environment of various games, developers can extend the lifecycle manager. Taking mobile QQ as an example, it is extended as follows:

```typescript

// Mobile QQ has registered this variable appInBackgound, making statement in the TypeScript statement, thus prevent error reporting
declare interface Window {

    appInBackgound:boolean;
}

egret.lifecycle.addLifecycleListener( (context)=>{
    
    // Method 1: Notify through event monitoring
, function(e:any){
        if (e.hidden){
            context.pause();
        }
        else{
            context.resume();
        };
    });

    // Method 2: Make judgment in each frame
    context.onUpdate = ()=> {
        if (window.appInBackgound){
            context.pause();
        }
        else{
            context.resume();
        }
    }
} )
```
