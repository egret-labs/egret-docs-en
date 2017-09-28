In the network communication, besides simple text data, some image resources, audio resources and so on will also be added.

In the request for different formats of data, different processing methods need to be developed. In Egret, there are five available data formats, namely:

1. Binary format

2. Text format

3. URL encoding format

4. Bitmap texture format

5. Audio format.

The above five data format settings are the required `URLLOaderDataFormat` class. If you want to change the default text format, you can modify the `dataFormat` attribute in` URLLoader`. The specific sample code is as follows:

```
class NetDemo extends egret.DisplayObjectContainer
{
    public constructor()
    {
        super();
        this.addEventListener(egret.Event.ADDED_TO_STAGE,this.onAddToStage,this);
    }
    private urlloader:egret.URLLoader;
    private onAddToStage(event:egret.Event)
    {
        this.urlloader = new egret.URLLoader();
        this.urlloader.dataFormat = egret.URLLoaderDataFormat.VARIABLES;
        var urlreq:egret.URLRequest = new egret.URLRequest();
        urlreq.url = "http://httpbin.org/headers";
        this.urlloader.load( urlreq );
        this.urlloader.addEventListener(egret.Event.COMPLETE, this.onComplete, this);
    }
    private onComplete(event:egret.Event):void
    {
        console.log( this.urlloader.data );
    }
}   
```

Among them there is a line:

```
this.urlloader.dataFormat = egret.URLLoaderDataFormat.VARIABLES;
```

The format of the loaded data is modified and set to the "URL encoding" format.

Run after compilation, with the effect shown as below:

![](568b4313ae75c.png)