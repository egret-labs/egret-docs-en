## 1. Use
Egret provides the `ImageLoader class class for loading bitmap files.

For example, the `ImageLoader` class loads the image at 'resource / egret.png' through the following code: 

``` TypeScript
var imgLoader:egret.ImageLoader = new egret.ImageLoader;
imgLoader.once( egret.Event.COMPLETE, this.imgLoadHandler, this ); 
imgLoader.load( "resource/egret.png" );  
```

In the defined callback event, you can use the following method to obtain the BitmapData corresponding to the image, and thus to create a bitmap:

``` TypeScript
imgLoadHandler( evt:egret.Event ):void{
    let loader:egret.ImageLoader = evt.currentTarget;
    let bmd:egret.BitmapData = loader.data;
    let texture = new egret.Texture();
    texture.bitmapData = bmd;
    let bmp:egret.Bitmap = new egret.Bitmap(texture);
    this.addChild(bmp);
}
```

## 2. Cross-domain processing

* Server sets up access permissions
* Anonymous access can be made by trying to modify `imgLoader.crossOrigin = 'anonymous'`. But cross-domain issues will be reported when `texture.toDataURL` is used.
* Webgl rendering does not support cross-domain image processing.