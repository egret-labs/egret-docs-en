Set the order in which event listeners are executed by prioritizing events.

You can prioritize events when registering listeners.
```
public addEventListener(type:string, listener:Function, thisObject:any, useCapture:boolean = false, priority:number = 0)
```

Set priorities need to set up `priority` properties. This property is of type number, and the higher the number, the higher the priority. The higher the priority when the event is triggered, the earlier the execution.