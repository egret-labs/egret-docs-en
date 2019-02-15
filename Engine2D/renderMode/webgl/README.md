## 1.*Introduce*

> WebGL is a standard graphics library for rendering 2D and 3D graphics.The standards are developed by Khronos, AMD, Ericsson, Google, Mozilla, Nvidia and Opera.

WebGL adds a JavaScript binding to OpenGL ES 2.0,Hardware 3D accelerated rendering for HTML5 Canvas. Egret Engine 2D provides a WebGL rendering mode.

WebGL provides the underlying rendering API,For traditional Web developers, the use of WebGL API is relatively complex, and a lot of knowledge related to OpenGL ES needs to be supplemented. I,However, using WebGL in Egret Engine is easy, just choose to enable WebGL rendering at the beginning of the application.

There is no need to worry about WebGL standard compatibility. If WebGL rendering mode is enabled, the browser will automatically switch to Canvas rendering mode if it is not supported.

### WebGL compatibility

Rendering with WebGL allows for hardware acceleration and improved performance.So you want to be able to use WebGL rendering in all environments. WebGL is now gaining more and broader support.

| PC browser | Compatibility |
|---|---|
| Chrome | Chrome 8 is now supported. |
| Firefox | WebGL is supported by default in Firefox 4 and above. |
| Safari  | Safari 5.1 support (Lion version is already available). |
| Opera | Opera 12 alpha and above. |
| IE | IE 11 start support. |

| Mobile browser | Compatibility |
|---|---|
| ChromeAndroid | Chrome 30 begins to support on devices that support the GL_EXT_robustness extension |
| Tencent x5 kernel | QQ browser and x5 TBS 2.x: webgl function is not supported under android 4.0, and above 4.0 will check according to the phone's gl instruction to finally decide whether to open webgl function |

## 2.Use

### Enable WebGL rendering

You can find the index. HTML file in the Egret project root. This file is the entry to the Egret project and contains the initialization Settings.

In index. HTML, we have a Egret startup function. If you want to enable WebGL rendering, pass in the parameters as follows.

```
egret.runEgret({renderMode:"webgl"});
```

You can also specify the render mode to be Canvas:

```
egret.runEgret({renderMode:"canvas"});
```

The default rendering mode is webGL.

### Determine the current render mode

Can pass  `Capabilities` class `renderMode` to judge the current rendering mode.

```
console.log(egret.Capabilities.renderMode);
```

On a single line of code will be printed on Canvas mode `canvas`,will be printed in WebGL mode `webgl`;

### WebGL with dirty rectangles

Due to compatibility issues with some browsers, rendering of dirty rectangles is currently closed under WebGL.

### Other matters needing attention

You can open WebGL in the Egret program's entry. If the browser does not support WebGL rendering, it will automatically switch to Canvas rendering mode.

Performance improvements can be achieved using WebGL rendering.However, in the case of a lot of text and vector graphics, there may be more overhead and will not improve performance.Because in WebGL rendering mode, text and vector drawing need to be cached in Canvas and then rendered to WebGL. Due to the process of Canvas rendering, if a large number of text or vector drawing is used, the corresponding performance improvement will not be achieved.

If you want to use under the WebGL `Texture` object  `toDataURL()` method convert Texture to base64 string, then the Texture images should be on the same server, refer to a different server resources will not be successful.

Of course, the WebGL standard is gaining ground, and some features on the phone aren't very friendly yet.Non-chrome browsers on mobile phones do not yet have very good support for irregular masks, which can be avoided when using WebGL renderers.




