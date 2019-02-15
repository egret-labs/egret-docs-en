Egret Engine 5.2 adds support to WeChat mini-game and QQ mini-game, and these project have a new project structure and unable to auto update with `egret upgrade` command, so developer needs to manually update engine version.

##### 1.Create a new project with Egret Engine 5.2
We add a `scripts` directory in project structure, which is a newly-added plugin system in Engine 5.2 version and will expand engine’s compiling and publish functions as well as the publish and configure functions of WeChat mini-game.
##### 2.Copy the codes and resources from older projects to new project such as `src` and `resource` directory.
* If the older projects use `EUI` library, please do not replace the `src/ThemeAdapter.ts` file in the new project.

##### 3.Configure the third-party library in `egretProperties.json` of the new project, use the same method in Egret engine 5.0

* `res` is the resource management module by default of project in 5.0 version. And we use the new version `assetsmanager` by default in 5.2 project, this module supports WeChat mini-game publish, and has compatible `API` and `res`, basically do not need to modify codes. If your project does not have the need to publish to WeChat mini-game, you can feel free to continue to use the older `res` module.

##### 4.Modify tsconfig.json
![](./p1.png)
`tsconfig.json` is the configuration file of `typescript` compiler, which is used to specify the compiling options of this project. 
As we shown aforementioned, `tsconfig.json` configuration is different in Egret Engine 5.0 series and 5.2 series.


* 5.0 series is `exclude`, which specifies those directories that do not participate compiling.
* 5.2 series is `include`, which specifies those directories that participate compiling.

For more detailed information please refer to [tsconfig Microsoft official documents](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/tsconfig.json.md)

If you cite third-party library in 5.2 project, you will need to configure in `egretProperties.json` and `tsconfig.json`.

![](./p2.png)
The picture aforementioned is a configuration demo of a game project of our own, it uses `egret-ps` and `egret-ps-wechat-tiny` two libraries.