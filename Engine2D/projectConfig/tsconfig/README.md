
`tsconfig.json` is the configuration file for Typescript project, Typescript compiler will firstly read it and set project’s compilation parameters based on its properties before compiling the code.



### Usage Mode

1 ) When it creates egret project, it will auto generate "tsconfig.json" text file in the root directory of the project.

2 ) Here we can see the engine parameter by default shown as below, you can modify them based on your project needs:

```
{
    "compilerOptions": {
        "target": "es5",
        "outDir": "bin-debug",
        "experimentalDecorators": true,
        "lib": [
            "es5",
            "dom",
            "es2015.promise"
        ],
        "types": []
    },
    "include": [
        "src",
        "libs"
    ]
}
```

Now let’s have a detailed description about the fields in `compilerOptions`.

* `target`: the standard that JavaScript files generated after compilation must follow is `es5` by default, it has a better compatibility and we do not recommend you to modify it.
* `outDir`: the compiled js files are stored in `bin-debug` directory, it’s not available to modify now.
* `experimentalDecorators`: enable experimental grammar decorators, some of the libraries in the engine use the latest grammar and need to enable this configuration.
* `lib`: compile you desired library file, there are 3 files by default, you can add files based on your needs.
* Other common parameters
	* `"sourceMap": true`: when we compile `.ts` file into `.js` file, it will generate a corresponding `.js.map` file, which enable developer to debug ts file directly in the browser.
	* `"removeComments": true`: delete the comments in the original `.ts` file when compiling `.js` file.
	


3 ) Set other fields, for example the `include` field, it’s at the same level with `compilerOptions` and means the files that will participate in the compilation. This field is `exclude` in engine `4.x` and previous version, and means the files that will not participate in the compilation.


4 ) Execute `egret build` command, you can compile egret project based on the configuration file.

For more detailed compilation parameters please refer to [tsconfig.json official documents](http://json.schemastore.org/tsconfig)。

TypeScript detailed manual reference：[TypeScript Handbook（Chinese Version）](https://www.gitbook.com/book/zhongsp/typescript-handbook/details)
