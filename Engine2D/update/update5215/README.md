# 白鹭引擎 5.2.15 发布日志


===============================

Update Time：March 4, 2019

## 2D Rendering - JavaScript

* The loading processes get stuck when loading audio resources on IE11
* HttpRequest increase support for `timeout` properties

## AssetsManager
* In Assetsmanager, the `Res.getResByUrl` method must be called after `loadConfig`. If called before this, the program will be misreported to abort the run. Now optimize the experience and note the error message instead, but the program can continue to run.

## WeChat Game v1.1.10
* Automatically replace with `fixedWidth` mode when the adapter mode is a `showAll` that is not supported by the platform
* Fix the `egret.Capabilities.os` has been returning to `iOS`
* Optimization, the engine frame frequency is not 60fps, the screen will appear flashing problems.


## Baidu Game v0.1.4
* Automatically replace with `fixedWidth` mode when the adapter mode is a `showAll` that is not supported by the platform
