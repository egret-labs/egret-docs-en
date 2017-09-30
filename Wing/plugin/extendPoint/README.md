The extension point allows the developer to customize some of the extensions in the wing. Define the extension point via the `contributes` field of the [`package.json`](../../../Wing/plugin/configDes/README.md) plugin.The following extension points are currently supported


* [`commands`](#contributescommands)
* [`keybindings`](#contributeskeybindings)
* [`configuration`](#contributesconfiguration)
* [`languages`](#contributeslanguages)
* [`cdebuggers`](#contributesdebuggers)
* [`grammars`](#contributesgrammars)
* [`themes`](#contributesthemes)
* [`snippets`](#contributessnippets)
* [`jsonValidation`](#contributesjsonvalidation)
* [`views`](#contributesviews)

## contributes.commands

Custom command `command`.The defined commands can be found and executed in the Command Palette.

> ** Note: ** [`activationEvent`](../../../Wing/plugin/activation/README.md) `onCommand:${command}` will be dispatched when the command is executed via the shortcut key or the command panel.

The following fields are available:

Name | Required | Type | Description
---- |:--------:| ---- | ------
`command` | is the unique id representing |`string`| by |`string`|
`title` | is the name used by | `string` | to represent command. This attribute will be displayed in the command panel.


### Example

```
...
"contributes": {
	"commands": [{
		"command": "extension.sayHello",
		"title": "Hello Wing"
	}]
}
...
```

![commands extension point example](5682053c729e0.png)


## contributes.keybindings

Customize shortcut `keybinding`.You can customize the bindings of keys that perform the command.

> ** Note:** You can define shortcuts for various operating system platforms.

> ** Note: ** [`activationEvent`](../../../Wing/plugin/activation/README.md) `onCommand:${command}` will be dispatched when the command is executed via the shortcut key or the command panel.

The following fields are available:

Name | Required | Type | Description
---- |:--------:| ---- | ------
`command` | is the id of the command bundled by |` string` | shortcut key
`key` | Yes |` string`> Shortcut key combination of keys. For the character strings that can be used for key combination, please see Appendix 1.
`win` |   | `string` | The key combination under Windows platform. If the user is under Windows, this attribute will override the key combination specified by the `key` field.
`mac` | |` string` | The key combination under Mac platform. Ff the user is under Mac, this attribute will override the key combination specified by the `key` field.
`when` | |` string` | For the expression of when the shortcut key will be triggered and the available attribute values, please refer to Appendix 2.


### Appendix 1 The rules for strings for the key combinations that can be used in the `key` field 

The Key rules are generally composed of key combinations + other keys. 

The combination of keys are as follows:

Operating system | Combination of Keys
---- | ---------
MACOS X | `ctrl+`, `shift+`, `alt+`, `cmd+`
Windows | `ctrl+`, `shift+`, `alt+`, `win+`

> ** Note: ** Specially, `ctrlcmd` can be used for representing the` ctrl` under Windows and the `cmd` under Mac


The other keys are as follows:

* `f1-f15`, `a-z`, `0-9`
* `` ` ``, `-`, `=`, `[`, `]`, `\`, `;`, `'`, `,`, `.`, `/`
* `left`, `up`, `right`, `down`, `pageup`, `pagedown`, `end`, `home`
* `tab`, `enter`, `escape`, `space`, `backspace`, `delete`
* `pausebreak`, `capslock`, `insert`


Use the key sequence divded by spaces. For example, (ctrl + k ctrl + c) means that ctrl+k shall be pressed first, and then ctrl+c, so as to trigger this shortcut key.

If you want to make a command can be triggered by ctrl+k and ctrl+c, please define two groups of keybindings, in which command is the same while the key field is different.


### Appendix 2 Character strings available in `when` field 

`when` fields can restrict conditions by using such expressions as `!`, `&&`, `==` and `!=`.Such as

`!inDebugMode`  , `editorTextFocus && editorLangId == 'ts'` are all available expressions.



* When `editorFocus` editor gets focus
* When `editorTextFocus` editor gets focus
* `editorLangId` represents the editor's language id, `editorLangId` usually corresponds to the document extension of corresponding editor 
* `inDebugMode` means when debugging is started

For more fields, please wait for the follow-up updates.

### Example

`Under Windows the shortcut key is `Ctrl+F1`, under Mac the shortcut keys is `Cmd+Shift+F1`:

```
...
"contributes": {
	"keybindings": [{
		"command": "extension.sayHello",
		"key": "ctrl+f1",
		"mac": "cmd+shift+f1",
		"when": "editorTextFocus"
	}]
}
...
```

## contributes.configuration

Provides the settable options, so that the user can modify these settings in the global or workspace settings.

Plug-in developers need to provide a set of JSON schema to describe these configurable options, so that users can get smart tips from the editor when modifying.

You can read the user-defined configuration information in the following way
`wing.workspace.getConfiguration('myExtension')`.

### Example

```
...
"contributes": {
	"configuration": {
		"type": "object",
		"title": "TypeScript configuration",
		"properties": {
			"typescript.useCodeSnippetsOnMethodSuggest": {
				"type": "boolean",
				"default": false,
				"description": "Complete functions with their parameter signature."
			},
			"typescript.tsdk": {
				"type": "string",
				"default": null,
				"description": "Specifies the folder path containing the tsserver and lib*.d.ts files to use."
			}
		}
	}
}
```

## contributes.languages

Provide a new language message so that EgretWing can support its development.

In this section, language generally refers to an id relevant to the file name (See `TextDocument.getLanguageId ()`).

EgretWing offers three methods to determine the language in which a file is used. These three methods can be used independently
1. file extension (hereinafter referred to as 'extensions')
2. file name (Hereinafter referred to as `filenames`)
3. The text in the first line of the file (Hereinafter referred to as `firstLine`)

The last information the Wing needs is the aliases of the language: alias of the language, the first of which will be displayed as the language's display name, which is displayed in the lower right corner of the editor and the language selection list.

When the user opens a file, Wing will use the three rules to match the file, so as to determine the file used by the language. At the same time, Wing will throw an activationEvent `onLanguage: $ {language}` (for example, the following example `onLanguage: python`) to activate the corresponding plugin.


### Example

```
...
"contributes": {
	"languages": [{
		"id": "python",
		"extensions": [ ".py" ],
		"aliases": [ "Python", "py" ],
		"filenames": [ ... ]
		"firstLine": "^#!/.*\\bpython[0-9.-]*\\b"
	}]
}
```
## contributes.debuggers

Provides a debug adapter for Wing, so as to help Wing connect to an external debug service, and extends Wing's debugging capabilities.

The debug adapter runs in a separate process, using a specific protocol to communicate with Wing.You need to provide at least one executable script to implement this debug adapter.


### Example

```
...
"contributes": {
	"languages": [{
		"id": "python",
		"extensions": [ ".py" ],
		"aliases": [ "Python", "py" ],
		"filenames": [ ... ]
		"firstLine": "^#!/.*\\bpython[0-9.-]*\\b"
	}]
}
```

## contributes.grammars

Provide a set of TextMate grammar to add language support for Wing.You need to provide the language `language`, grammar' TextMate` scopeName` value and the path of grammar definition file, which are required by this set of grammar to fit 

> ** Note: ** The format of the grammar definition file can be either JSON (extension .json) or XML plist format (if the extension is not json, it is thought as this format).

### Example

```
...
"contributes": {
	"grammars": [{
		"language": "shellscript",
		"scopeName": "source.shell",
		"path": "./syntaxes/Shell-Unix-Bash.tmLanguage"
	}]
}
...
```

## contributes.themes

Provide a TextMate theme code color matching theme.You need to specify a `label` to indicate whether the theme is dark or light. There is also the theme file path (XML plist format)


### Example

```
: {
"themes": [{
"label": "Monokai",
"uiTheme": "vs-dark",
"path": "./themes/Monokai.tmTheme"
}]
}
```

## contributes.snippets

```
: {
"snippets": [{
"language": "go",
"path": "./snippets/go.json"
}]
}
```

## contributes.jsonValidation

Provide JSON schema of a specific json file. `url` can be plug-in built-in file, or a remote url, such as [json schema store] (http://schemastore.org/json)

```
: {
: [{ 
"fileMatch": ".jshintrc",
"url": "http://json.schemastore.org/jshintrc"
}]
} 
```

## contributes.views

** Tips **: This extension point requires EgretWing version> = 3.0.6

Register a `webview` panel in a specific view.The `url` provided can be a file built in the plugin, or a remote url.Currently registering panel on the right side of the column is supported.

The following fields are available:

Name | Required | Type | Description
---- |:--------:| ---- | ------
`type` | is the type of |` string` | panel. Currently only `utility` is supported
`id` | is the unique id of |` string` | panel.
`title` | is the name displayed by | `string` | panel.
`url` | Yes | the corresponding url link or `html` path of | `string` | `webview`.
`order` | No |` number` | The order that the panel is displayed in the current Part.
`icon` | No |` string`> The icon to be displayed on the panel tab.

### Example

```
: {
: [{
"type": "utility",
,
,
,
./web/index.html
}]
} 
```

