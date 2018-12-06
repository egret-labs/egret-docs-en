##  JS Communications with Java

###  JS to Java Messaging

Java registers methods to receive messages:

```java
nativeAndroid.setExternalInterface("sendToNative", new INativePlayer.INativeInterface() {
    @Override
    public void callback(String message) {
        String str = "Native get message: ";
        str += message;
        Log.d(TAG, str);
    }
});
```

JS sends a message:

```javascript
egret.ExternalInterface.call("sendToNative", "message from JS");
```

###  JS to Java messaging

Java registers methods to receive messages:

```javascript
egret.ExternalInterface.addCallback("sendToJS", function(msg) {
    console.log(msg);
});
```

JS sends a message:

```java
nativeAndroid.callExternalInterface("sendToJS", "message from Java");
```

### Pay attention to
You need to register the method that receives the message to receive the message sent by the other end.

At the start of the application, JS may not have finished loading, which is not acceptable when sending a message to JS. You can send a message to Java in the game code to inform the Java side that the receiving method has been registered,and then send a message to JS.

##  JS Communicates with OC

The logic is the same as Android,except that the API for the native project is different.

### Native

How to register to receive messages:

```objective-c
[_native setExternalInterface:@"sendToNative" Callback:^(NSString* message) {
    NSString* str = @"Native get message: ";
    str = [str stringByAppendingString:message];
    NSLog(@"%@", str);
}];
```

Send message:

```objective-c
[_native callExternalInterface:@"sendToJS" Value:@"message from OC"];
```
