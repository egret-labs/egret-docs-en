EgretWing loads the plugin by means of inactive load. The `activate` method defined by the plugin will be invoked only when the plugin needs to be activated. Through the `activationEvents` field of the [`package.json`] (../../../Wing/plugin/configDes/README.md) of the plugin, a context is provided to indicate when the plugin will be activated. The following activation events are currently supported:

* [`onLanguage:${language}`](#activationeventsonlanguage)
* [`onCommand:${command}`](#activationeventsoncommand)
* [`workspaceContains:${toplevelfilename}`](#activationeventsworkspacecontains)
* [`*`](#activationevents*)

## activationEvents.onLanguage

This event will be triggered when the document of corresponding language is opened. For example:

```json
...
"activationEvents": [
	"onLanguage:python"
]
...
```

## activationEvents.onCommand

The event will be triggered when a command `command` is executed. For example:

```json
...
"activationEvents": [
	"onCommand:extension.sayHello"
]
...
```

## activationEvents.workspaceContains

The event will be triggered when the workspace includes the specified file. For example:

```json
...
"activationEvents": [
	"workspaceContains:.editorconfig"
]
...
```

## activationEvents.*

The event will be triggered when EgretWing is started. For example:

```json
...
"activationEvents": [
	"*"
]
...
```