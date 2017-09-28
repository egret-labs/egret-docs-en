
The configuration file named ```egretProperties.json``` is included in the root folder of the project, and the configuration involved in the engine is stored here.

### The whole frame

![image](5604f755ba98b.png)

### egret_version field

The version of the egret command line currently used by the project.

### modules field

Define all library files referenced in the project.
Each library is the configuration information in the form of ```{ "name":"moduleName" , "path":"modulePath"}```.	
```name``` field is the library name.```path``` field is the library file storage path. If this field isn't available, take the default value ```$ {EGRET_DEFAULT}```

``` json
{
	"egret_version":"5.0.6",
	"modules":[
		{
			"name":"egret",
		},
		{
			"name":"tween",
			"path":"${EGRET_APP_DATA}/4.0.3"
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

`` `` path``` field can include library file version number

	There are two environmental variables in the Egret Engine:
	`` `EGRET_DEFAULT``` represents the path of the current engine.
	`` `EGRET_APP_DATA``` represents the path in the cache folder in the engine launcher.
	In the above configuration file, the ```egret``` module of the engine will use the path corresponding to the version configured in ```egret_version```, and the ```tween``` module will use the path corresponding to the 4.0.3 version downloaded in the engine launcher.
	In this way, developers can selectively upgrade the specific module of the engine, thereby reducing the potential stability risk resulting from the version upgrade.


The path corresponding to the ```path``` field may be inside or outside of the project. 

* If it is inside the project, the library corresponding to this path is loaded directly when running the project.
* If it is outside of the project, the library corresponding to this path will first be copied to the ```libs/modules``` folder inside the project when compiling the engine. Then, the library inside the folder will be loaded.

After modifying the contents of the configuration, you need to execute the ```egret clean``` command for reconstruction, so as to ensure the changes take effect.

### Publish field
The configuration file required to publish the project.

* path: the directory where the published file is located. The default value is "bin-release".

* web: The method for publishing Web project resource file.0, publish according to the name of the original material path; 1. The resources will be published after it is renamed after crc32 naming method.The default is 0.

* native: The method for publishing Native project resource file.0, publish according to the name of the original material path; 1. The resources will be published after it is renamed after crc32 naming method.The default is 1.

In RES module provided by Egret, the supported publishing method is web = 0, native = 1. If you need to customize the version control, please modify the corresponding publishing method.

### template field
If : {} ``` field is available, use the template, otherwise the template needn't be used

### eui field
eui project related configuration

* exmlRoot:  Specify the root directory for exml file storage, which must be a relative path.It would be best if the directory only includes exml file. If other files are also included, the compilation speed will be affected.

* themes: The theme file array, which configures all the theme file paths that must be relative paths.

* exmlPublishPolicy: the strategy used by the theme file for storing exml when publishing, including path, content and gjs


	path: the theme file only stores the path and will load different exml files. It is not recommended when it is the same as debug
	content: the theme file stores exml content and won’t load different exml files. The advantage is that the whole file is smaller
	gjs: the theme file stores the js content that has been compiled by exml, and won’t load different exml file. The advantage is fast resolution


### native field
native-related configuration, which is only useful for native projects. This field can be ignored when the Web project is published.

* path_ignore: the list that shall be ignored when the project material is copied to the publishing directory, the string value of which will be parsed into a regular expression.
For example, set the value of this field to "anim.* ons".
The project resource file directory is as follows:
![image](5604f756594ae.png) 
The published resource file directory is as follows:
![image](5604f7562d513.png)

* android_path (the field that can be ignored): the directory of the created android project will be automatically created when android project is created.

* ios_path (the field that can be ignored): the directory of the created ios project will be automatically created when ios project is created.

### web field
web configuration, which is only useful for web projects. This field can be ignored when the Native project is published.
* path_ignore: (4.0.0 or above is supported) the list that shall be ignored when the project material is copied to the publishing directory.


### urlParams field (3.1.6 or above is supported)

* As for the ```egret run``` command, add URL parameters. For example, open the address after implementing ```egret run```:

```http://10.0.4.63:3001/index.html?okok=12&id=455464564```
