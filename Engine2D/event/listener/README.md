An event listener, or handler of an event, is responsible for receiving the information carried by the event and executing specific code upon receipt of the event.

In Egret, the listener for the event must be a function. Event sender must be  `egret.EventDispatcher` class or subclass instance. Only event senders can listen for events, and listeners can be registered.

Listener events are divided into two parts. The first is to set up a listener, which can be a separate function or a method of an object. The second step is to register the listener, use the event sender `addEventListener()` assigned to the corresponding event listener.

Here is the definition of the registered listener function.

```
public addEventListener(type:string, listener:Function, thisObject:any, useCapture:boolean = false, priority:number = 0)
```


* `type`：event type, must choose.

* `listener`： used to handle the event listener, will choose.

* `thisObject`：scope, must choose, fill in this general. Because TypeScript and JavaScript have different this scopes, they also have different this directions. If you don't fill in this, the compiled code gets an error. For this question, learn about the prototype chain in JavaScript.

* `useCapture`: make sure the listener is running in the capture phase or running in the bubbling phase, optional. Set to true, the listener processes events only during the capture phase, not during the bubbling phase. Set to false, the listener only processes events during the bubbling phase.

* `priority`： event listener priority, optional. The priority is specified by a signed integer. The larger the number, the higher the priority. All listeners of priority n are processed before those of priority n-1. If two or more listeners share the same priority, they are processed in the order in which they were added. The default priority is 0.

### 1.Create a listener

The listener must be a function, which can be a stand-alone function or an instance method. The listener must have a parameter, and this parameter must be an instance of the Event class instance or its subclass, and the listener's return value must be void. The sample code is as follows:

```
listenerName(evt:Event):void {...}
```

### 2.Register and remove listeners

Only event sender can register a listener, the sender must be `EventDispatcher` instances of the class or subclass. The same is true for removing listeners. Typically, registering and removing listeners come in pairs.

Register listeners

```
event sender.addEventListener(event type, listener, this);
```

Remove listener

```
event sender.removeEventListener(event type,listener, this);
```

### 3.Detect the listener

If you need to detect in your logic whether an event sender has registered a listener, there are two methods you can use. One is `hasEventListener` ,another was a `willTrigger` 。Both methods perform the same function, determining whether an event sender has registered an event of a certain type.

If the event type has already been registered, return `true`，if has not been registered, return `false`。

```
event sender.hasEventListener(event type);
```

### 4. Startup switch of TouchEvent

Start switch of TouchEvent  `touchEnabled` specify whether this object to receive touch or other user input. The default value is false, and the instance will not receive any touch events (or other user input events).If the  `touchEnabled`is set to true, then the display object instance will receive touch events, or other user input events. To change the display of all child objects touchEnabled behavior, please use the `DisplayObjectContainer.touchChildren`。

In actual use, if some display object needs to listen for TouchEvent, please open it first:In actual use, if some display object needs to listen for TouchEvent, please open it first: In actual use, if some display object needs to listen for TouchEvent, please open it first:
```
Display object instances.touchEnabled = true;
```
