Egret loads resources mainly through the `egret.HttpRequest` class.This class encapsulates the `XMLHttpRequest` object used as an H5 standard for asynchronous loading of resources and communications.

This section is mainly about loading static files, which is divided into two types: text and binary data.
Loading static files is characterized by the ability to track progress.

## 1. Load the text   

The core method of `HttpRequest` object is `open ()` and `send () `.  The `open ()` method receives the URL to which the request will have access. As an option, the load mode can also be passed. This parameter usually takes the constant with `HttpMethod`, which is the most commonly used GET method by default.       
When the load is completed, the `response' property of the` HttpRequest` object gets the returned data.    
The method for loading text data is as follows:   

```
var url = "resource/config/description.json";
var  request:egret.HttpRequest = new egret.HttpRequest();
        
var respHandler = function( evt:egret.Event ):void{
   switch ( evt.type ){
       case egret.Event.COMPLETE:
           var request:egret.HttpRequest = evt.currentTarget;
           console.log( "respHandler:n", request.response );
           break;
       case egret.IOErrorEvent.IO_ERROR:
           console.log( "respHandler io error" );
           break;
   }
}
        
var progressHandler = function( evt:egret.ProgressEvent ):void{
   console.log( "progress:", evt.bytesLoaded, evt.bytesTotal );
}

request.once( egret.Event.COMPLETE, respHandler, null);
request.once( egret.IOErrorEvent.IO_ERROR, respHandler, null);
request.once( egret.ProgressEvent.PROGRESS, progressHandler, null);
request.open( url, egret.HttpMethod.GET ); 
request.send( );
```
`HttpRequest` The default load type is TEXT, so no special settings are required.
The main event that needs to be intercepted is `COMPLETE`, which gets the data from here.   
To take into account the unexpected situation, do this in IO_ERROR.
The load progress event is `ProgressEvent.PROGRESS`, which is useful when loading the resource of large contents.

## 2. Load binary   
The method of loading binary data is as follows:

```
var url = "resource/assets/egret_icon.png";
var  request:egret.HttpRequest = new egret.HttpRequest();
request.responseType = egret.HttpResponseType.ARRAY_BUFFER;

var respHandler = function( evt:egret.Event ):void {
   switch ( evt.type ){
       case egret.Event.COMPLETE:
           var request:egret.HttpRequest = evt.currentTarget;
           var ab:ArrayBuffer = request.response;
           console.log( "respHandler:n", ab.byteLength );
           break;
       case egret.IOErrorEvent.IO_ERROR:
           console.log( "respHandler io error" );
           break;
   }
}

request.once( egret.Event.COMPLETE, respHandler, null);
request.once( egret.IOErrorEvent.IO_ERROR, respHandler, null);
request.open( url, egret.HttpMethod.GET );
request.send( );
```
Load binary data. First, set the `HttpRequest` load type as `ARRAY_BUFFER`.   
After the data is loaded, you can take the `ArrayBuffer` object from the `response` property to make a further read operation.  

> Build a communication request via `URLLoader`. Please visit:
[URLLoader network communication] (../../../extension/game/URLLoaderNetwork/README.md)
`The URLLoader` class has been moved to the game extension library.