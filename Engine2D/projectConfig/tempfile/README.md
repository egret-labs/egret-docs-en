There is a `template` folder in the root directory of Egret 5.2.x project, which has two directory

### Web
If there is `template` field in your project’s configuration file `egretProperties.json`, then `template/web/index.html` will be used as the entry file when the `Html5` project is published.
For example:

```
{
  "engineVersion": "5.2.9",
  "compilerVersion": "5.2.9",
  "template": {}, //As long as this field exists,
  //System will use template/web/index.html as entry file.

  ...
 }
```

### Runtime
Publish the configuration file of the native project



### Version change
`5.0.8`: the version update script will delete the `template/debug` folder, the `5.0.8` or higher version engine will not use `template/debug/index.html` as template. Developers can directly modify the index.html file of the project.

`5.0.1`:`template/debug` is used for debug, `template/web` is used for publish