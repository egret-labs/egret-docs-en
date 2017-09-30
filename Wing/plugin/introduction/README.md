The EgretWing plugin project is based on `NodeJS` and can be written in the `TypeScript` language.EgretWing provides a set of API interfaces that allow developers to customize some functionalities of EgretWing.

## Necessary development environment

- [Download the latest Wing](https://egret.com/en/products/wing.html) 。
- NPM command line tool, NodeJS installation package with `npm` command line tool.


## Create a new plug-in project

Open the menu, select `File - New project - extension item, and create a plugin project.
The new project also provides several sample projects to showcase some basic usage of API.
- WebView is created with a custom UI plugin.When you need a large number of user interaction scenarios, you can use WebView to create a flexible interface.
- TextTools gets text editor's related information and manipulate the text editor content.
- OneDarkTheme creates a theme item with custom Code coloring.


## Use EgretWing to develop plug-in projects


### Install dependency package

If the plugin project needs to rely on other nodejs modules, it needs to be executed under the root directory of the project

npm install

Install the dependency module.


### Compile the project

Use the default shortcut `Ctrl/Cmd + Shift + B` to compile the project.


## Plugin directory structure description

After all the above operations are completed, you can see the following directory structure.

```
.
├── .gitignore
├── .wingignore                 // A list of files that will be excluded when a plugin is published
├── .wing
│   ├── launch.json             // Debug starts the configuration file
│   ├── settings.json           // Project settings file
│   └── tasks.json              // Task configuration file
├── images
│   └── icon.svg	            // The plugin icon
├── node_modules                // Dependency module
│   ├── .bin 
│   ├── egretwing               // Contains plugin api, installation, compilation and other script modules
│   ├── typescript
│   └── semver
├── typings                     // .d.ts catalogue
│   └── index.d.ts              // Referenced plugin API
├── extension.ts                // ts source code
├── package.json                // Plugin description file
├── README.md
├── tsconfig.json               // ts compilation configuration
```

- `egretwing` module is a module needed for development, which defines a .d.tsfile that includes plugin api.In the `typings` directory you can reference the required `.d.ts`

- `package.json` is a description file of the plugin. For more information, please see: [Description file](../../../Wing/plugin/configDes/README.md)

)

## More examples

We have posted some common plugins and examples on GitHub for reference.Project address:

https://github.com/egret-labs/wing-extensions

