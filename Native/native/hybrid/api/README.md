# The iOS API Documentation
```
 The unit of all file sizes is byte
```

## EgretWebViewLib

### Initialize
```
+ (void)initialize:(NSString*)preloadPath;
preloadPath: Cache the root directory (the cache directory is under Documents and needs to start and end with '/')
```

###  Listen for Game Callbacks
```
+ (void)setExternalInterface:(NSString*)funcName Callback:(ExternalInterfaceBlock)block;
funcName: Name of the callback
block: The callback method

Game call method: window["ExternalInterface"].call(funcName, value)
```

###  Call the Method Registered in the Game
```
+ (void)callExternalInterface:(NSString*)funcName Value:(NSString*)value;
+ funcName:  Method names
value: parameter

Callback method for game registration:window["ExternalInterface"].addCallback(funcName, callback)
```

###  Start the Local Server

Start the server from the pre-download directory

```
+ (bool)startLocalServer;
Return value: whether successful or not
```

Start the server directly from the Resource directory (0.1.11 add)

```
+ (bool)startLocalServerFromResource;
Return value: whether successful or not
```

### Start the Game
```
+ (void)startGame:(NSString*)gameUrl SuperView:(UIView*)superView;
gameUrl: The game is the address
superView:  The parent View
```

You can also specify the server address of the game, and resources that do not exist locally will be downloaded from the server (0.1.12 added).

```
+ (void)startGame:(NSString*)gameUrl Host:(NSString*)host SuperView:(UIView*)superView;
gameUrl: The game is the address
host: Server address
superView: View The parent View
```

### Stop the Game
```
+ (void)stopGame;
```

> If the local server is enabled: the game is loaded from the pre-cached directory when the game is started, and the local server is stopped when the game is stopped. Stop the game

### Gets the cache directory size
```
+ (long long)getCacheSize;
Return value: directory size
```

### Gets the Cache Directory Location
（0.1.12added）

```
+ (NSString*)getPreloadPathByGameUrl:(NSString*)gameUrl;
gameUrl: The game is the address
Return value: the absolute path to the cache directory
```

### Clean up Cache Directory
```
+ (void)cleanPreloadDir;
```

### Check Whether a Resource Has Been Loaded
```
+ (bool)checkLoaded:(NSString*)resUrl;
resUrl:  Links to resources

+ (bool)checkLoaded:(NSString*)zipPath Host:(NSString*)host;
zipPath: zip    The absolute path to the file
The resource in the host: zip file is mapped to which url path, ending with "/". Example:"https://www.game.com/egret/" 
```

### Create the Download Task
```
+ (ListFileLoader*)createListFileLoader:(NSString*)resUrl Delegate:(id)delegate;
+ (ZipFileLoader*)createZipFileLoader:(NSString*)resUrl Delegate:(id)delegate;
resUrl: Links to resources
delegate: Listens for the object of the callback

+ (ZipFileLoader*)createZipFileLoader:(NSString*)zipPath Host:(NSString*)host Delegate:(id)delegate;
zipPath:The absolute path to the zip file
host: The resource in the file is mapped to which url path, ending with "/". Example:"https://www.game.com/egret/"
delegate: Listens for the object of the callback
```

### Stop all Download Tasks
```
+ (void)stopAllLoader;
```

### The Destruction
```
+ (void)destroy;
```

## ZipFileLoader, ListFileLoader

### Start
```
- (void)start;
```

## FileLoaderProtocol

### Start the Download
```
- (void)onStart:(long)fileCount Size:(long)totalSize;
fileCount:  The number of files
totalSize: Total download size
```
>  onStart is the first callback

###  Download Progress
```
- (void)onProgress:(NSString*)filePath Loaded:(long)loaded Error:(long)error Total:(long)total;
filePath: The file path
loaded: Number of downloaded files (json mode); Downloaded size (zip mode)
error: Number of files that failed to download (json mode)
total: Total number of files (json mode); Zip file size (zip mode)
```

### Error
```
- (void)onError:(NSString*)urlStr Msg:(NSString*)errMsg;
urlStr:  Address of the file
errMsg: The error message
```

###  Download the End
```
- (void)onStop;
```
>  OnStop is the last callback

### Unzip
```
- (bool)onUnZip:(NSString*)zipFilePath DstDir:(NSString*)dstDir;
zipFilePath: The file path
dstDir: The target directory
Return value: whether decompression succeeded
```
>  Considering that different developers may have their own decompression libraries, there is no integrated decompression function.
