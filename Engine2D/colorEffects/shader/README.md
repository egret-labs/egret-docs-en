
### 1.Introduction

In Egret 5.0.3 and higher version, official provides `egret.CustomFilter` for developers to freely extend the filter to achieve a variety of custom effects.
> This feature is only available in web and micro-client environments.


`CustomFilter` we need to introduce the string of vertex shader and fragment shader program, as well as the `uniforms` object.

* Developers can write their own vertex shader and fragment shader programs based on project requirements.

* The properties of `aVertexPosition`，`aTextureCoord`，`aColor`，`projectionVector` in vertex shader are introduced by engine

* Engine will upload the properties of `uniforms` object to shader before its rendering. The developers can alter the properties of the ‘uniforms’ object on every frame scale to achieve requirements of different effects. This property currently only supports numbers and arrays.

* `egret.CustomFilter` also provides `padding` property, which is the padding of the filter, if the custom filter required area is larger than the original area (such as the stroke filter provided by the engine), you need to manually set the property, and this property takes pixel as unit.

For more detailed instructions please refer to[API documents](http://developer.egret.com/cn/apidoc/index/name/egret.CustomFilter#methodSummary)。

### 2.Practical Tutorial

Look at the following example, we implements the effect of a black and white square background. First we create a game project, then we insert the vertex shader code at the end of the createGameScene function in Main.ts:

```
let vertexSrc =
	"attribute vec2 aVertexPosition;\n" +
	"attribute vec2 aTextureCoord;\n" +
	"attribute vec2 aColor;\n" +
	
	"uniform vec2 projectionVector;\n" +
	
	"varying vec2 vTextureCoord;\n" +
	
	"const vec2 center = vec2(-1.0, 1.0);\n" +
	
	"void main(void) {\n" +
	"   gl_Position = vec4( (aVertexPosition / projectionVector) + center , 0.0, 1.0);\n" +
	"   vTextureCoord = aTextureCoord;\n" +
	"}";
```

Then we insert fragment shader code:

```
let fragmentSrc =
    "precision lowp float;\n" +

    "varying vec2 vTextureCoord;\n" +

    "uniform float width;\n" +
    "uniform float height;\n" +

    "void main(void) {\n" +
    "vec4 fg;\n" +
    "if(mod(floor(vTextureCoord.x / width) + floor(vTextureCoord.y / height), 2.0) == 0.0) {" +
    "fg = vec4(1,1,1,1);" +
    "}" +
    "else {" +
    "fg = vec4(0,0,0,1);" +
    "}" +
    "gl_FragColor = fg;\n" +
    "}";
```
In the aforementioned code, we define the width and height of each square, and these two value are introduced by `uniforms` property. Then based on uv information and the introduced width and height, and calculate parity number by using the remainder function, and whether the square is black or white is determined by the parity.

Use a custom filter to the background image, set the size of each square as 50 pixels:

```
let size = 50;
let filter = new egret.CustomFilter(vertexSrc, fragmentSrc, { width: size / stageW, height: size / stageH });
sky.filters = [filter];
```

The effect is shown as below image, here we can see that the background image becomes a square of alternating black and white, each square size is 50 pixels.

![](heibai.png)

Then we can change the size of square (uniforms property) through the frame function:

```
let inc = 1;
this.stage.addEventListener(egret.Event.ENTER_FRAME, function () {
    size += inc;
    if (size >= 80) {
        inc = -1;
    }
    if (size <= 50) {
        inc = 1;
    }
    filter.uniforms.width = size / stageW;
    filter.uniforms.height = size / stageH;
}, this);
```

Run the game again, and we can see that the size of each frame will change accordingly

Visit [Here](http://developer.egret.com/cn/example/egret2d/index.html#210-egret2d-heibai) to see the aforementioned demo.

Visit [Here](http://developer.egret.com/cn/example/egret2d/index.html#210-egret2d-customefilter) to see more demo.