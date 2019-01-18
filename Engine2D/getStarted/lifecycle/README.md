
In game, player users can switch the app from the front to the back end. To ensure a better user experience, you can set to turn off game logic, render logic, and background logic after user’s app is switched to the back end.



Egret Engine introduced the Lifecycle Manager since version 4.1, ```egret.lifecycle```. Its code example is shown below:

```typescript
egret.lifecycle.onPause = ()=> {
    console.log("app enter the back end");
    egret.ticker.pause(); // Turn off rendering and heartbeat
}
egret.lifecycle.onResume = ()=> {
    console.log("app enter the front end");
    egret.ticker.resume(); // open rendering and heartbeat
}
```

For different game running environment, developers can operate extension to lifecycle manager, taking mobile QQ as an example, its extension is shown as below:

```typescript

// The mobile QQ registered appInBackgound variable, and declared it in TypeScript to prevent error report
declare interface Window {

    appInBackgound:boolean;
}

egret.lifecycle.addLifecycleListener( (context)=>{
    
    // Method 1: notify by means of event monitoring
    document.addEventListener("qbrowserVisibilityChange", function(e:any){
        if (e.hidden){
            context.pause();
        }
        else{
            context.resume();
        };
    });

    // Method 2: judge from each frame
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
