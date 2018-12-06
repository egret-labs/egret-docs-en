
You may find some problems, such as blank screen and connot run correctly after packaging, when you package and run Android App.  Here, you need to use logcat debugging function of Android to detect problems.

It will pop up automatically Android tabs when you run Android project in IntelliJ, shown as the figure below:

![](568a5d4b14058.png)

In normal conditions, it will display all log of the entire system, but we can make it only display the output log of the app that's we're debugging by using the process filtering function. Select the button and the app process we want to debug:

![](568a5d4b320ca.png)

But there may still be a lot of unwanted information, even if we have limited an app process. Don't be sad, we can do a further filteration based on log types:

![](568a5d4b40959.png)

Warn and Error are the most common log kinds we use, for these two contain information that needs to be checked first when the program is not working properly.

