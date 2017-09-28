## 1. Use
Egret provides the `ImageLoader class class for loading bitmap files.

For example, the `ImageLoader` class loads the image at 'resource / egret.png' through the following code: 

``` TypeScript
var imgLoader:egret.ImageLoader = new egret.ImageLoader;
imgLoader.once( egret.Event.COMPLETE, this.imgLoadHandler, this ); 
 );  
```

In the defined callback event, you can use the following method to obtain the BitmapData corresponding to the image, and thus to create a bitmap:

``` TypeScript
imgLoadHandler( evt:egret.Event ):void{
    var loader:egret.ImageLoader = evt.currentTarget;
    var bmd:egret.BitmapData = loader.data;
    var bmp:egret.Bitmap = new egret.Bitmap( bmd );
    this.addChild(bmp);
}
```

## 2. Cross-domain processing

* Server sets up access permissions
* Anonymous access can be made by trying to modify `imgLoader.crossOrigin = 'anonymous'`. But cross-domain issues will be reported when `texture.toDataURL` is used.
* Webgl rendering does not support cross-domain image processing.