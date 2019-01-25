
## 1.Introduction

* Ts is a super set of js, so as long as those js and js can call each other, ts can also call them, but it needs to add declaration to solve the error report in compiling.

* the generated file of ts is js, so js calling ts is actually js calling js (ts generated js file).

## 2.ts calling js

### Steps

* Find the method of js calling js.

* Add declaration of method call. Please refet to [how to produce .d.ts](http://developer.egret.com/cn/github/egret-docs/extension/threes/dts/index.html) 。

### Demo

* Method in js

~~~
function callJsFunc(msg) {
	console.log("msg from egret : " + msg);
}
~~~

* Declaration in ts

~~~
declare function callJsFunc(msg:string);//can be placed in ts file (it’s suggested that you put it on top or bottom, we had not try to put it in the middle area) or placed it a separate .d.ts file, please do not put it in other types of files. The msg types is judged by the function body.
~~~

* call in ts

~~~
callJsFunc("hello js");
~~~

* output

~~~
msg from egret : hello js
~~~


>Summary: add declaration based on js calling js. Others, such as variables, are also implemented by the aforementioned steps. 


## 3.js call ts

Calling ts is actually ts calling ts, since ts calls ts, there may be abbreviated writing style in the same module, so just use the call in different modules to write.

### Steps

* Find ts call in a different module （such as  ```example.A.CallEgretFunc("hello")```）。

* Write exactly as the aforementioned method (such as the aforementioned ```example.A.CallEgretFunc("hello")```)。

### Demo

* Method in ts

~~~
module exampleA {
    export class A {
        public callEgretMethod(msg:string):void {
            console.log("method msg from js : " + msg);
        }

        public static CallEgretFunc(msg:string):void {
            console.log("static msg from js : " + msg);
        }
    }
}
~~~


* ts call in a different module

~~~
module exampleB {
    export function b() {
    	//call method
    	var a:exampleA.A = new exampleA.A();
    	a.callEgretMethod("method");
    	
    	//call static function
    	exampleA.A.CallEgretFunc("function");
    }
}
~~~



* call in js


~~~
var a = new exampleA.A();//Remove the type of a 
a.callEgretMethod("method");

exampleA.A.CallEgretFunc("function");
~~~

* output

~~~
method msg from js : method
static msg from js : function
~~~

> Summary: it’s same as ts calls ts in a different module. Others such as variables are also implemented as aforementioned steps.
