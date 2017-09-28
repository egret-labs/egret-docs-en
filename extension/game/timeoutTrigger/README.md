## 1. Start the timeout trigger

There is a need to run an event after running for a certain period of time.For example, a dialog box needs to automatically disappear a few seconds after certain prompt is displayed.

`egret.setTimeout` provided by Egret can achieve the above functions.The prototype of the function is:

```
function setTimeout(listener: Function, thisObject: any, delay: number, ...args: any[]): number;
```

* `listener` is the callback function to be executed
* `thisObject` is set to` this`
* `delay` sets the number of milliseconds for timeout waiting,
* `... args` is the parameter of random number, or you can also have no parameter.

The following example demonstrates how to use the timeout trigger:

```
var idTimeout:number = egret.setTimeout( function( arg ){

        console.log( "timeout:", arg );	, arg );

    }, this, 3000, "egret"	egret

);

console.log( "start setTimeout" );	 );
```

Compile and run. First, output "start setTimeout". There will be "timeout: egret" after three seconds, which indicates that the trigger is running accurately.

## 2. Stop the timeout trigger

In the case of a timeout, there may be a need to stop the timeout trigger. Then, as shown in the above example, the timeout trigger needs to be canceled if the user touches the dialog box's Close or OK button before the timeout expires. Egret provides `egret.clearTimeout` to cancel the timeout trigger.A `id: idTimeout` is returned when `egret.setTimeout` is implemented and the id is used to cancel the timeout trigger:

```
egret.clearTimeout( idTimeout );
```

The timeout trigger will be stopped if the statement is executed before timeout waiting ends. The callback function will no longer be executed.

When the timeout waiting is over, the callback function will be executed immediately, and subsequent execution of `egret.clearTimeout` will no longer make sense.

Note: The `egret.setTimeout` and `egret.clearTimeout` used in this tutorial are under the `egret` package, which is the timeout trigger achieved by Egret engine and shall not mix with javascript's own `setTimeout` and `clearTimeout`. That is, the implementation of timeout `id` returned by `egret.setTimeout` can not be stopped with javascript's own `clearTimeout`, and vice versa.
