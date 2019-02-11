## 1.`egret.RenderTexture`

Bitmaps in egret are displayed based on textures, and there are usually four ways to draw a static texture:

* Get the texture property directly from the Bitmap you've created.

*  Through `RES.getRes("run_down_png");`directly obtained (if there is a use of Res module)

* Obtained after loading by URLLoader

* The bitmapData of the Texture object is assigned a value of the obtained data by the ImageLoader loader.

Besides, egret provides dynamic texture class`egret.RenderTexture`，used to display object and its children will draw a texture, in order to realize the screenshot function.

```
var renderTexture:egret.RenderTexture = new egret.RenderTexture();
renderTexture.drawToTexture(displayObject);
```


## 2.Methods

### 2.1.toDataURL()
The`egret.RenderTexture` `toDataURL()`methods，convert texture into "data:image/png;base64," begins the base64 data.

Usage  `texture.toDataURL("image/png", new egret.Rectangle(20, 20, 100, 100));`

* The first parameter is the format you want to convert to, and currently only “image/png” and “image/jpeg” are supported.

* The second parameter is the capture area, the default for`texture`whole size。

> Note：
Because of `texture`itself, the interception of conversion, so even if `Bitmap`zooming operations such as deformation, also won't affect `texture`  interception area size.

### 2.2.saveToFile()
The `egret.RenderTexture   saveToFile()`  methods，cutting the designated area and save into images.

Usage：`texture.saveToFile("image/png", "a/down.png", new egret.Rectangle(20, 20, 100, 100));`

* The first parameter is the image format

*  The second parameter is the name of the saved file (the path).

* The third parameter is the truncated area

>  Note：
The browser only supports saving names, so when you write "a/down.png", the browser automatically changes it to "a-down.png". The image will be saved in the browser download location.

> Path can be saved under Native. The image will be saved in the game private space, path can not have.. / ".
In order to be compatible with all platforms, it is recommended not to use paths.

#### The sample
Save the screenshot test, the code is as follows:

```
var texture:egret.Texture = RES.getRes("run_png");
texture.saveToFile("image/png", "a/down.png", new egret.Rectangle(20, 20, 100, 100));
```

Here are using `saveToFile()`generated views.

The original image

![](55cd9c0ddeeb5.png)

Interception of complex

![](55cd9c0e37c9a.png)

### 2.3.drawToTexture()

 The   `egret.RenderTexture   saveToFile()` methods，object map will display as a texture

It is important to note that this method will reduce the current texture clear, if you want to keep the previous texture, need to use 2   `RenderTexture` alternating drawing.

Used interchangeably  `RenderTexture` sample code:

```
if (this.bmp.texture == this.renderTexture) {
    this.renderTexture2.drawToTexture(this, new egret.Rectangle(0, 0, 1024, 768));   
    this.bmp.texture = this.renderTexture2;
} else {
    this.renderTexture.drawToTexture(this, new egret.Rectangle(0, 0, 1024, 768)); 
    this.bmp.texture = this.renderTexture;
}
```

The  `this.bmp` is to save the bitmap object sketchpad,`this.renderTexture` and `this.renderTexture2` is used to store grain `RenderTexture` object.

Update drawing board texture with different from current`RenderTexture` object to ensure the last texture will not be empty.

## 3. Screenshot of the sample

click on[Dynamic screen](http://developer.egret.com/cn/example/page/index#040-bitmap-draw)，you can view the complete code and effect of dynamic screen sample.
