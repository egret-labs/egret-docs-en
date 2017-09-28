
Set the current workspace under the `.wing / tasks.json` can customize the task.The common tasks include building, cleaning up and publishing, etc.These tasks are usually implemented by executing a command line program.
If the `.wing` folder under the current workspace does not have` tasks.json`.You can use the **Tasks in the command panel: The Configure Task Runner ** command selects a task template.

![](5.png)

For the general Egret projects, the task that matches the Egret command line has been automatically generated when the project is created: ** build (Ctrl + Shift + B), clean up, publish**.`tasks.json` is as follows:

```
{
    "version": "0.1.0",
    "command": "egret",
    "isShellCommand": true,
    "suppressTaskName": true,
    "tasks": [
        {
            "taskName": "build",
            "showOutput": "always",
            "args": [
                "build",
                "-sourcemap"
            ],
            "problemMatcher": "$tsc"
        },
        {
            "taskName": "clean",
            "showOutput": "always",
            "args": [
                "build",
                "-e"
            ],
            "problemMatcher": "$tsc"
        },
        {
            "taskName": "publish",
            "showOutput": "always",
            "args": [
                "publish"
            ],
            "problemMatcher": "$tsc"
        }
    ]
}
```
