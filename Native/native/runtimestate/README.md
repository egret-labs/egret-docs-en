# Runtime Event Callback During Runtime

## state

- Message type

```
{"state”:”starting”}  index Load the success
{"state”:”running”}  js Load successful, start to run the game
```

- Register for listening (take Android as an example)

```java
private void setExternalInterfaces() {
    // handle the state change Event during the running
    nativeAndroid.setExternalInterface("@onState", new INativePlayer.INativeInterface() {
        @Override
        public void callback(String message) {
            String str = "Native get onState message: ";
    
            str += message;
            Log.e(TAG, str);
        }
    });
}
```

## error

- Message type

```
{"error":"load"}  index Load failed
{"error":"start"}  js Load failed
{"error”:”stopRunning”}  An exception occurs during the run that interrupts the engine's heartbeat (typically jsError is thrown first)
```

- Register for listening (take Android as an example)

```java
private void setExternalInterfaces() {
    // handle the error Event during the running
    nativeAndroid.setExternalInterface("@onError", new INativePlayer.INativeInterface() {
        @Override
        public void callback(String message) {
            String str = "Native get onError message: ";
    
            str += message;
            Log.e(TAG, str);
        }
});
```

## jsError

- Register for listening (take Android as an example)

```java
private void setExternalInterfaces() {
    // handle the error Event during the running
    nativeAndroid.setExternalInterface("@onJSError", new INativePlayer.INativeInterface() {
        @Override
        public void callback(String message) {
            // Parameter is stack information
            String str = "Native get onJSError message: ";
    
            str += message;
            Log.e(TAG, str);
        }
});
```
