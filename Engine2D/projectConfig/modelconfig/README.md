
In the project profile `egretProperties.json`， `modules` fields can be defined all the library files referenced in the project.

Each library is shaped like a  `{ "name":"moduleName" , "path":"modulePath"}` configuration format.
`name` field is the library name，`path` field is the library file storage path,

 The library file version number can be included in `path`   fields

The `path`  for the field may be in or out of the project. The library file version number can be included in the fields

* If you are in a project, the project runtime directly loads the library corresponding to this path.
* If outside the project, the engine compile this path is first library copy of the corresponding to the project's  `libs/modules`  folder, and then load the library in this folder.

 There are two types of engine libraries

**Built-in library**，including:

* `egret` Engine core library
* `egret3d` Engine 3 d library
* `assetsmanager` Resource management module
* `dragonBones`  DragonBones
* `eui` EUI  Component library
* `game` The game  library
* `media`  The multimedia library
* `socket` Websocket network communication library
* `tween` Slow motion gallery

Built-in libraries can omit `path`  fields, the default and  `egret_version` using the same version. Can also be `path` fields in separate setting the library using version

** The third-party library **

Egrets official offers some [common third-party libraries](https://github.com/egret-labs/egret-game-library) for developers to use.

Developers can also configure their own libraries in the project.

Usage example:

```
{
	"egret_version":"5.2.6",
	"modules":[
		{
			"name":"egret",
		},
		{
			"name":"tween",
			"path":"${EGRET_APP_DATA}/5.0.3"
		},
		{
			"name": "particle",
			"path": "../libsrc"
		},
		{
			"name": "promise",
			"path": "./promise"
		}
	]
}
```
This configuration represents:

* Module uses  `egret_version`  5.2.5 
*  The `tween` uses Versions  5.0.3 
*  The path of the `particle`  module is outside the project
*  The path to the `promise` module is in the project

