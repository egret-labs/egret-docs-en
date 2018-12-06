## Preparation

1、Learn about the solution of packaging native project via  egret-ios-support,

2、Learn the basic operations in Egret project, and the basics programming skills of iOS and Android.

You can have a test by creating a new HelloWorld project after learning the aforementioned basics.

In Egret, we use global class`ExternalInterface` to communicate with `native`.

3、Get Sample Project

After downloading Egret Android Support and Egret IOS Support, we can find the template project of HelloEgret in corresponding directory.

You can find the source codes of Egret Android Support in path `proj.android\src\org\egret\java\HelloEgret`

You can find the source codes of Egret IOS Support in path `egret_ios_template\proj.ios\HelloEgret`

## Native Sending Message to Egret

### Egret Message Listener

It listens messages from `Native` via `addCallback` method of `ExternalInterface`

```
// TypeScript Code
egret.ExternalInterface.addCallback("sendToJS", function (message:string) {
    console.log("message form native : " + message);//message form native : message from native
});
```

In aforementioned codes, we call the first parameter "sendToJS" to represent the function name that's sent from `Native` terminal. The other parameter is callback function, it will call the callback function when `Native` terminal sends message, where `message` is the value sent by  the `Native` terminal.

### Sending Message  in Native

It's relatively easy that sending message to Egret in native codes, we can send message to Egret via corresponding API. Here it contains two parameters, the first is `ID` of sending message, the other is value of sending message. When it listens the same `ID` message in Egret, it will receive the message and trigger a callback. Here the `sendToJS` we listened in Egret is the `ID` of sent message.

The message sending codes of Android
```
// Java Code
// Instantiating gameEngine in onCreate 
gameEngine.callEgretInterface("sendToJS", "message from Android");
```

The message sending codes of iOS

```
/// Objective-C Code 
[[EgretRuntime getInstance] callEgretInterface:@"sendToJS" value:@"message from IOS"];
```

## Egret Sending Message to Native

### Native Message Listener

#### Message Listener in Android

Listening message in Android is conducted by calling `EgretGameEngine` instance's  `setRuntimeInterface` method. The first parameter still is the listen-needed ID, and the second parameter needs to instantiate a `IRuntimeInterface` and rewrite its `callback` method, in which receives strings of callback.

Firtly we need to implement `IRuntimeInterface`:

```
private interface IRuntimeInterface {
    public void callback(String message);
}
```

The message listening codes of Android:
```
// Java Code
//Instantiating gameEngine in onCreate
gameEngine.setRuntimeInterface("sendToNative", new IRuntimeInterface() {
           @Override
            public void callback(String message) {
                Log.d("externalInterface", "message : " + message);
            }
        });
```

#### Message listener in iOS

iOS part is cooresponding to code receiver, it's also relatively easy of listening callback in iOS part,  here we also call `setRuntimeInterface`, the two parameters are respectively listening ID `sendToNative` and callback function.


The message listening codes of iOS:
```
/// Objective-C Code 
[[EgretRuntime getInstance] setRuntimeInterface:@"sendToNative" 
    block:^(NSString * message) {
        NSLog(@"message :%@", message);
    }];
```

### Sending Message  in Egret

It sends messages to `native` via `call` method in `ExternalInterface`. The two parameters in `call` are respectively `functionName` and `value`, note that these two parameters are string type. `functionName` represents the function callback name that we call in Native terminal, you can also see this parameter as ID of the function callback, thus you can use this name to distinguish callback functions when multiple funcitons are needed to be called in Native terminal. However,  the `value` parameter is relatively easy to understand, it represents the specific value that's sent to Native terminal.

```
// TypeScript Code
egret.ExternalInterface.call("sendToNative", "message from js");   
```
In aforementioned codes, we sent a message `message from js` to `Native`, and native will receive this messge in its callback function when we added `sendToNative` listener in `Native` terminal.