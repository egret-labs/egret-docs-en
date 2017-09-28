The Egret Engine supports the construction of library projects, and developers can package reusable logic into a library, so as to reuse between different projects.

This document is for the Egret Engine version 4.1+

### Build a third-party library method

* Open a third-party library folder
* Remove the modoules field in ```package.json```
* Create a ```tsconfig.json``` file at the same level as ```package.json``` in the project
* Modify the ```tsconfig.json``` file and implement different project configuration according to different types of class libraries of TypeScript/JavaScript:

```
// JavaScript class library
{
    "compilerOptions": {	: {
        "target": "es5",	,
        "outFile": "bin/libtest1/libtest.js",	,
        "allowJs": true	: true
    },	    },
    "files": [	: [
        "src/a.js",	,
src/b.js
    ]
}
```

```
// TypeScript class library
{
    "compilerOptions": {	: {
        "target": "es5",	,
        "outFile": "bin/libtest1/libtest.js",	,
        "declaration": true	: true
    },
    "files": [	: [
        "src/a.ts",	,
src/b.ts
    ]
}
```

* If the project is a JavaScript class library, you need to configure a ```typings``` field in ```package.json``` and set it as a custom .d.ts file, as shown below:


```
/** Project structure
libtest
    |-- src
    |-- bin
    |-- typings
            |-- libtest.d.ts
    |-- tsconfig.json
    |-- package.json 
*/

// package.json
{
    "name": "libtest",	,
typings/libtest.d.ts
}
```

* After the above operation, the implementation of egret build will generate library files, compressed files and .d.ts files based on the ```outFile``` field in ```tsconfig.json````