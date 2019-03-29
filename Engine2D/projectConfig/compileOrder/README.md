In Egret, you write programs that use TypeScript and ultimately compile to browser-readable JavaScript.

JavaScript is a scripting language that the browser executes in the order of the scripts. , in fact, the browser will according to  `<script>`  label script loading in order to execute the script. When a script references a variable in an unloaded script, the browser reports an error.

In general, in a Egret project, you do not need to manually deal with the compilation order, because the Egret compiler helps the developer deal with it. But in one case the compiler can't deal with it, the need to manually add   `<reference>`  tags to tell the compiler class dependencies in the project. The following is the specific code and the solution.

TypeScript detailed manual reference：[TypeScript Handbook（Chinese）](https://www.gitbook.com/book/zhongsp/typescript-handbook/details)

### Test dependencies

A new Egret project, used here  `egret create test`  create an Egret project by default.

Several test classes are established. The structure of the project is as follows:

![](56e7b0cb40856.png)

As shown above, a Test folder is created, a Call folder is created internally, and testcall.ts is created within Call.Create both testa.ts and testb.ts in the Test folder. The rest of the Main. Ts and LoadingUI. Ts etc. are not needed here and can be ignored here.

The code in testa.ts is as follows:

```
class TestA{
    public static arr:Array<any> = ["t","e","s","t","c","a","l","l"];
}
```

The code in testb.ts is as follows:

```
class TestB{
    public static testBStr:string = TestA.arr.join("");
}
```

Both classes have only one static member.The TestA class holds an array, and the TestB class concatenates the contents of the array into a string and saves it. So far our compile run has found no exceptions.

Add a call to the TestB class in testcall.ts.

```
class TestCall{
    public static test:any = egret.getDefinitionByName(TestB.testBStr);
}
```

Compile run after found that the browser will report the following `TestB.js:11 Uncaught ReferenceError` error：

![](56e7b0cb4fc18.png)

When we added  `TestB.testBstr`  found after the call browser TestA class has not been defined, leading to testBstr this property page can't find it. Examining the resulting index.html file after compilation reveals that testb.js is loaded before testcall.js and testa.js is loaded last. The browser will report an error when testb.js calls the contents of the file in testa.js.

The above invocation relationship is obviously valid in the code, and the compiler does not report an error. The compiler does not generate the correct loading order, mainly because it cannot confirm the order in which static members of such a class reference each other. Testb.js is automatically loaded before testcall.js when the contents of testb.ts are referenced in testcall.ts. This occurs because a reference to a static member of testa.ts in testb.ts cannot be detected.

###  The solution

The solution to this situation is to tell the compiler about the class dependencies in the project. Used in TypeScript `<reference>` label to represent the reference relationship. The relative paths of dependent files can be marked in the reference tag. So just add the following comments before the TestB class:

```
///<reference path="TestA.ts" />
```


```
class TestB{
    public static testBStr:string = TestA.arr.join("");
}
```

This usually happens with static member references, but there are other cases where this can happen with minimal probability. If you do, add a dependency tag to tell the compiler how to load it correctly.