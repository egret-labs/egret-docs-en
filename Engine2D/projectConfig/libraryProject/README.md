# The Third Party Extension Library

## Preparation 

The third-party library can be a standard ts library, or the ready-made js library that you download, or the js library that developer wrote by themselves. 

Due to the difference in syntactic structure between js and ts, you cannot directly call the API of js library in ts, so the TypeScript team provides us a set of fictitious declaration grammar, which can describe the API of the existing code in the form of a header file with the extension name of d.ts (with the use of d.ts naming method, it will remind the compiler that this file does not need to be compiled). This set of fictitious definition grammar enable developer do not need to implement code in the function body, similar to defining interface and abstract classes.

Fortunately, most popular js libraries are currently provided by official, and their corresponding d.ts files are provided by those enthusiastic community developers. However, if you cannot find your desired one, you can write it by yourself. For more details, please refer to[JS class library and methods for managing these libraries](https://github.com/vilic/typescript-guide/blob/adaaef2281150e57657e5b67368f592a968fad8f/%E5%85%A5%E9%97%A8%E6%8C%87%E5%8D%97/%E4%BD%BF%E7%94%A8JS%E7%B1%BB%E5%BA%93.md)。 

In addition, since some popular js libraries have quick update rate, it might happen that the found d.ts file definition is inconsistent with the version of js library, then lead a not exactly match situation for the within API. In this case, we either look for the corresponding version of the js library, or modify the d.ts file by ourselves.

For the detailed modification method, other than taking comparison of the original d.ts, you may need to learn the grammar about ts interface, for more info please refer to [ts interface tutorial](http://bbs.egret.com/thread-885-1-1.html)。 





## Create a third-party library 

When we have prepared the third-party library that’ll be used, we also need to compile it into the module structure that Egret engine needs.

1. Create a project file for Egret’s third-party library, enter it on the command line:

   ```bash
   egret create_lib demo
   ```

   After the execution is complete, we can see a newly-created demo file folder with two files `package.json`  `tsconfig.json`.

2. Then we create `src`   `bin`    ` typings` directory in demo file folder.

   There are two cases depending on the type library of TypeScript / JavaScript:

   #### TypeScript library

   Directly put ts file into src directory

   Modify `tsconfig.json`file：

   ```json
   {
       "compilerOptions": {
           "target": "es5",
           "noImplicitAny": false,
           "sourceMap": false,
           
           // If or not generate d.ts file. If the library type is typescript then set as true, if it’s javascript library then set as false.
           "declaration": true,  
           
           "outFile": "bin/demo/demo.js",  // the path of generated library file 
       },
       "include": ["src"]
   }
   ```

   ### JavaScript library

   Put the js file into `src` directory, and then put the corresponding .d.ts file into `typings` directory.

   modify`tsconfig.json`file：

   ```json
      {
         "compilerOptions": {
             "target": "es5",
             "noImplicitAny": false,
             "sourceMap": false,
      
             // If or not generate d.ts file. If the library type is typescript then set as true, if it’s javascript library then set as false.
             "declaration": false,  
      
             "outFile": "bin/demo/demo.js",  // the path of generated library file
      
             // If or not allow to compile js file. if it’s typescript library then set as false, if it’s javascript library then set as true.
             "allowJs": true  
         },
         "include": ["src"]
      }
   ```

      Modify `package.json` file：

      ```json
      {
          "name": "jszip",
          "compilerVersion": "5.2.7",
          
          // Add a new field
          "typings": "typings/demo.d.ts"
      }
      
      ```

  

   

3. Executing a command

   ```shell
   egret build demo
   ```

   Generate library files, compressed files and .d.ts files according to `outFile` field in `tsconfig.json`.

   The `demo` folder generated in the `bin` directory is the third-party library folder we can use.


### TIP

If you already have the three files: `demo.js`、`demo.min.js`、`demo.d.ts`, then you don’t need to implement the aforementioned steps, directly put these three files into the same folder and use it, that’s all.



## Use third-party libraries

1. Copy the `demo` folder to the project libs directory  (not to `modules`).

2. edit`egretProperties.json`file：

   ```json
   {
     "engineVersion": "5.2.7",
     "compilerVersion": "5.2.7",
     "template": {},
     "target": {
       "current": "web"
     },
     "eui": {
       "exmlRoot": [
         "resource/eui_skins"
       ],
       "themes": [
         "resource/default.thm.json"
       ],
       "exmlPublishPolicy": "commonjs"
     },
     "modules": [
       {
         "name": "egret"
       },
       {
         "name": "eui"
       },
       {
         "name": "assetsmanager"
       },
       {
         "name": "tween"
       },
       {
         "name": "promise"
       },
       
       
       // add a new field
       {
         "name": "demo",  // the third-party library’s name
         "path": "./libs/demo"  // path
       }
     ]
   }
   ```

3. Compile the Engine

   ```shell
   egret build
   ```

   Once executed, the imported third-party libraries will be available in the current project.





## The third-party library provided by the engine

Egret provides some useful third-party libraries, developers can download and use them by their needs.

* JSZip Library

  > Download: https://github.com/egret-labs/egret-game-library/tree/master/jszip
  >
  > Tutorials：http://developer.egret.com/cn/github/egret-docs/extension/jszip/jszip/index.html

* mouse support library

  > Download：https://github.com/egret-labs/egret-game-library/tree/master/mouse
  >
  > Tutorials：http://developer.egret.com/cn/github/egret-docs/extension/mouse/mouse/index.html

* P2 physical system library

  > Download：https://github.com/egret-labs/egret-game-library/tree/master/physics
  >
  > Tutorial：http://developer.egret.com/cn/github/egret-docs/extension/p2/p2/index.html

* Particle Library

  > Download：https://github.com/egret-labs/egret-game-library/tree/master/particle
  >
  > Tutorial：http://developer.egret.com/cn/github/egret-docs/extension/particle/introduction/index.html

* Tiled map library

  > Download：https://github.com/egret-labs/egret-game-library/tree/master/tiled
  >
  > Tutorial：http://edn.egret.com/cn/docs/page/718