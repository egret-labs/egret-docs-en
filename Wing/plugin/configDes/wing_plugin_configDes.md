Each plugin extension must store a `package.json` as the plugin item description file in the root directory of the plugin.

## field definition

Name | Required | Type | Description
---- |:--------:| ---- | ------
`name` | Yes |` string` | The name of the plugin extension, all of which are lowercase letters and no spaces.
`version` | Yes |` string` | reference [Semver] (http://semver.org/lang/). For example: `1.2.0`
`publisher` | Yes |` string` | publisher name
`engine` | Yes |` object` | contain the object of the `wing` field, define the version of the required environment.For example, `^ 3.0.0` means that 3.0.0 or higher is required.
`displayName` | |` string`| The name of the plugin.
`description` | |` string` | description of the plugin.
`icon` | |` string` | The icon used by the plugin is 128 * 128 in size.
`main` | |` string` | The relative path to the plugin entry, when the plugin starts, `activate` method of the entry file will be called.
`category` | |` string[] `| plug-in classification. The commonly used categories are: `[Languages, Text, Debuggers, Other]`.
[`contributes`](../../../Wing/plugin/extendPoint/README.md) | | object` | For the description objects of of the plug-in extension point, see [contributions] (../../../Wing/plugin/extendPoint/README.md).
[`activationEvents`](../../../Wing/plugin/activation/README.md) | | `string[]` | For the descriptive array of the plugin activation event, see [activation events](../../../Wing/plugin/activation/README.md).
`keywords` | |` string[] `| plugin keywords, accurate keywords is helpful for better finding the plugin.
The `Node.js` library on which `dependencies` | | `object` | plugin depends, see [npm dependencies](https://docs.npmjs.com/files/package.json#dependencies).
For the `Node.js` library on which `devDependencies` | | `object` | plugin development environment depends (For example, if the plugin is written using TypeScript, the development environment needs to depend on `typescript`, see [npm devDependencies](https://docs.npmjs.com/files/package.json#devdependencies).
The id of other plugins on which `extensionDependencies` | | `string[]` | depends on. The plugin id is `${publisher}.${name}`. For example: `egret.text-tools`.
`scripts` | | `object` | See [npm scripts](https://docs.npmjs.com/misc/scripts)

## Example

	{
		"name": "TextTools",
		"description": "Text replacement functions e.g. change case, reverse and ASCII Art.",
		"version": "0.2.0",
		"publisher": "egret",
		"categories":[
			"Other"
		],
		"icon": "images/TextToolsIcon.png",
		"bugs": {
			"url": "https://github.com/egret-labs/wing-extensions/issues"
		},
		"homepage": "https://github.com/egret-labs/wing-extensions/blob/master/README.md",
		"repository": {
			"type": "git",
			"url": "https://github.com/egret-labs/wing-extensions.git"
		},
		"activationEvents": [
			"onCommand:extension.textFunctions"
		],
		"engines": {
			"wing": "^2.5.0"
		},
		"main": "./out/extension",
		"contributes": {
			"commands": [
				{
					"command": "extension.textFunctions",
					"title": "Text Functions",
					"description": "Text functions on selections"
				}
			],
			"keybindings": [
				{
					"command": "extension.textFunctions",
					"key": "Alt+T"
				}
			]
		},
		"scripts": {
			"compile": "tsc -watch"
		},
		"dependencies": {
			"underscore.string": "^3.2.2",
			"figlet": "^1.1.1"
		},
		"devDependencies": {
		}
	}