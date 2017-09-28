
## 1. Package HTML5

HTML5 publishing process is as follows:

"1. Click the menu ""plug-in"" -> ""Egret project tool"" -> ""publish Egret project"", there will be a publish configuration dialog box, as shown below."

![](config.png)

* Version number, the name of the generated directory folder.
* Select the type of project to be published. Please select HTML5 here.
* Whether to merge image resources.If checked, the images in the project will be automatically merged.

"2. Click OK, the folder corresponding to the ""v1"" version will be generated in the publish directory of the project."

![](created.png)

3. Put the published on the server by just accessing index.html can.

## 2. Package Runtime

Accessing Runtime will greatly improve game performance.

Various cooperation channels on the Runtime platform can facilitate game promotion and converge the payment functions of various access channels.

For the specific steps of accessing Runtime, please refer to [Open Platform wiki] (http://open.egret.com/Wiki) and [Runtime Package Instructions] (http://open.egret.com/Wiki?mid=2&cid= 11).

## 3. Package Android app
> The Android Support that is based on Android Studio is a template for creating Android projects on Android Studio.The current template is a preview tutorial.

### 3.1.Mac package

#### Pre-preparation
1. Download and install Android Studio 2.1.2 or later.([Download] (http://pan.baidu.com/s/1c2dV3xe))

2. Download and install JDK 1.8 or later.([Download] (http://pan.baidu.com/s/1c2dV3xe))

3. Set the environment variable ANDROID_HOME

* cd ~/
* ls -a -l 
* Check if the above results include .bash_profile file, if not, please create this file with touch .bash_profile
* open. bash_profile You can do it just by writing the following statement in the file and replacing the path by yourself.Example: `export ANDROID_HOME=/Users/androidSDK/sdk`
* Execute source .bash_profile
* Echo $ ANDROID_HOME Check if you can output the corresponding path

Note:
1. Under very few cases, only restarting the computer can work.
2. This configuration is modeled on mac's default shell execution environment. If you are using other shell environments, please modify the corresponding configuration file. For example: please modify. Zshrc when zsh is used


#### Usage
The usage is the same as that of Android Support.Example:

`egret create_app HelloEgretAndroidAS -f HelloEgretH5 -t /Users/egret-android-support-3.2.0/egret-android-support-as-3.2.0`

> Since egret-android-support includes `eclipse` and `Android Studio` versions of the project, please ensure that you select the corresponding project when selecting tool.
> Folder name with 'as' is a `Android Studio` project, while folder name without 'as' is not a `eclipse` project.

#### Import project
1. Use Android Studio to import the generated project.Android Studio will check the project configuration and so on.Some components may be updated automatically.This may take certain time.

2. If the project doesn't match the current environment, Android Studio will provide the prompt for update and amendment step by step.Please update and amend the project configuration step by step.Android StudiO won't automatically update or amend the project configuration.Please delete proj.android/grandle file.Then import the project.According to the prompt, Android Studio will be allowed to configure and amend the project again.


3. Set the JD version used by the project.

![](577103c85caab.png)

![](577103c9c9d0e.png)

4. Once everything get ready, you can begin running and debugging。


### 3.2. Windows packaging

#### Pre-preparation
1. Download and install Android Studio 2.1.2 or later.（[Download](http://pan.baidu.com/s/1c2dV3xe")）

2. Download and install JDK 1.8 or later.（[Download](http://pan.baidu.com/s/1c2dV3xe")）	)）

3. Set the environment variable ANDROID_HOME

![](5771040e9d3d8.png)

![](5771040faf171.png)

![](57710410a0e22.png)

Then click OK.After completion, it is suggested to restart the computer.

#### Usage
The usage is the same as that of Android Support.Example:

`D:\egret-proje>egret create_app HelloEgretAndroidAS -f HelloEgretH5 -t D:\egret-android-support-3.2.0\egret-android-support-as-3.2.0\`

> Since egret-android-support includes `eclipse` and `Android Studio` versions of the project, please ensure that you select the corresponding project when selecting tool.
> Folder name with 'as' is a `Android Studio` project, while folder name without 'as' is not a `eclipse` project.

#### Import project
1. Use Android Studio to import the generated project.Android Studio will check the project configuration and so on.Some components may be updated automatically.This may take certain time.

2. If the project doesn't match the current environment, Android Studio will provide the prompt for update and amendment step by step.Please update and amend the project configuration step by step.Android StudiO won't automatically update or amend the project configuration.Please delete proj.android/grandle file.Then import the project.According to the prompt, Android Studio will be allowed to configure and amend the project again.

3. Set the JD version used by the project.

![](57710412332ee.png)

![](577104132cdf2.png)

4. Once everything get ready, you can begin running and debugging。

## 4. Package iOS app

egret-ios-support is as solution packaged by Egret for the original ios APP. egret-ios-support can help you package HTML5 game into ipa file, and provide the file for users to install.

This article will show you how to install the Egret core package, Egret's iOS support package in an environment where npm installation package has been installed. Ultimately, the Demo will be run in the simulator.

This article consists of three parts: the first part is the installation of the iOS development environment, the second part is for the installation of Egret game framework, and the third part creates a complete iOS App example.

### 4.1. Preparation of knowledge

In order to successfully complete this tutorial, please make sure you have the following knowledge:

* Understand the concepts of files, folders, and know how to create, move, copy, rename and delete.

* Understand one of the terminal, the command line and the shell and is capable of starting one of them. Also you shall be capable of competing the relevant operation of the previous item by means of command line implementation

* Learn how to download files and extract files

* Understand the following terms:

    * Writing game logic needs: JavaScript, TypeScript, nodejs, npm

    * Packaging iOS App needs: Objective-C, C ++, Xcode

> It is recommended to read [Get Started] (../../../Engine2D/getStarted/helloWorld/README.md)

### 4.2. Install iOS development environment 

#### Install the iOS development environment - Xcode

"Run the App Store, search for ""Xcode"" in the search items, download and install it"

![](56664988d7d76.png)

### 4.3. Install the Egret game frame

#### Prepare knowledge

Run the Terimal application for Mac OS X: Open the Applications folder in the Finder, open the Utilities folder, then find the Termial application, and double click Run.As shown below:

![](566649891032b.png)

"After entering the working directory, in the demo, the working directory is ""labs/"", and the working directory is an empty folder, as shown below:"

![](566649892b54a.png)

![](5666498952fbd.png)

Next, build a projects folder and run it

```
$ mkdir projects
```

As shown below:

![](56664989695f4.png)

![](566649898fba5.png)

#### Install Egret

Portal: [install the latest Egret under Mac OS X] (../../../Engine2D/projectConfig/installation/README.md).

#### Download Egret's iOS support package

Create the Egret Support folder

![](56664989b625e.png)

* Download Egret ios support package *

"Download [egret-ios-support](http://www.egret.com/downloads/ios.html)，and place egret-ios-support in the ""labs / egret-support /"" folder as shown below:"

![](56664989d5c4a.png)

### 4.4. Create an example of an iOS package

#### Create an Egret project

Create a project named `ACoolHtmlGame` with the following command:

```
$ egret create ACoolHtmlGame
```

As shown in the figure:

![](5666498a0f7f5.png)

![](5666498a4f6be.png)


#### Write a game item

Here we do not operate, instead, we demonstrate with the default project.

#### Create ios project

"Go back to the game project folder ""labs/projects/"" and create a project for ios with a new command that needs to specify the original HTML5 project and your egret-ios-support path when creating the project.The order is as follows:"

```
$ cd projects/
$ egret create_app ACoolIosGame -f ACoolHtmlGame -t ../egret-support/egret-ios-support
```

>The `create_app` command can be used to create a project suitable for ios.`ACoolIosGame` is the project name of the project.

`-f` parameter specifies HTML5 game project. You just need to enter the path of the newly created HTML5 project.

"The `-t` parameter is the template for the ios project, and you need to specify the"" egret-ios-support ""project path."

The following figure shows the running command demo:

![](5666498a7cff0.png)

After running the command, you will see the folder of the newly generated ACooliosGame project, which is structured as follows:


![](5666498aa996b.png)

Since then, you have created a complete ios project, with the current file level as follows:

```
labs/-+
      +-- egret-core/-+                         # egret
      +-- egret-support/-+                      # egret support library
      |                  +-- egret-ios-support/ # ios support
      +-- projects/-+
      |             +-- ACoolIosGame            # ios project
      |             +-- ACoolHtmlGame           # html application
      ...
```

#### compile iOS games

"Open the ACoolIosGame folder, double-click ""ACoolIosGame.xcodeproj"", and wait for Xcode to be loaded"

![](5666498ac908d.png)

#### Test the project

Click the Xcode Run command to go directly to the iOS emulator

![](5666498ae5860.png)

The following figure shows the operation effect

![](5666498b20f9b.png)

To generate the ipa package, please visit the [Apple Development Website] (http://developer.apple.com/), register the developer account, and read the relevant settings.

Since then, you have completed the whole process of achieving a iOS game application with Egret .

#### The overall process of project development

We recommend the following development method: develop in the original HTML5 game project, then develop and test successfully before compiling into the iOS platform.The demonstration of the process is as follows:

1. Create an HTML5 game:

`egret create ACoolHtmlGame`

2. Create the corresponding iOS game

`egret create_app ACoolIosGame -f ACoolHtmlGame -t ../egret-support/egret-ios-support`

3. Test the various platform games

4. Develop game in the ACoolHtmlGame, and then compile the game and test it on the browser, use

`egret build ACoolHtmlGame --runtime native -e`

This line executes two tasks: 1. Compile TypeScript to JavaScript, 2. Synchronize the compiled files into the Xcode project.There are two things to note: 1. The compiled project is a *HTML5 project; 2. Do not change the location of the iOS project*, and the project location settings will be offered in the advanced tutorial, 3. At this point the HTML5 project will be ineffective. If you want to view HTML5 items, please use 

`egret build ACoolHtmlGame -e`

To make the HTML5 project effective, the iOS project will become ineffective at this moment.

5. Then you can use egret startserver ACoolHtmlGame to start the game service, so that the browser will be able to observe the realized the game logic.

6. Then go back to the ACoolIosGame Xcode project, use Xcode to clear, recompile, debug the project, so that you can get on the phone the same game logic as that on HTML projects.

7. Return 4, constant iteration.

## 5. Package WinPhone app

Using the HTML5 games developed by Egret, you can package into WinPhone native APP program.

### 5.1. Create an Egret project

For details, please refer to [Get Started](../../../Engine2D/getStarted/helloWorld/README.md)

Because the encoding format supported by WinPhone packaging is UTF-8 +, but egret provided the UTF-8, so developers need to convert bin-debug (if the js code has been compressed, then bin -debug folder isn't needed for converting into files) and the files under launcher after copying files.(You can use the software that can convert file format in batch.For example, GB2UTF8 batch file encoding conversion tool v1.3). If the software does not allow UTF-8 to be converted into UTF-8 + or UTF-8 (with BOM), you can convert the files by converting UTF-8 (with BOM) through gb.

### 5.2. Run the egret project in VS

> egret Run the minimum configuration in VS: Windows8.1 and VS2013。

Here's how to create a VS project that supports the egret project, as well as the structure of the VS project.

![](568a5ce05b0cb.png)

![](568a5ce0830b5.png)

![](568a5ce0a11b6.png)

![](568a5ce0bd793.png)

After generating the VS project, you need to copy the bin-debug in the egret project (if the js code is compressed, the compressed file need not bin-debug folder), launcher, resources file folder under EgretWinExample.Shared/js folder

Select the code actually run the egret, and copy 

![](568a5ce0d1a2b.png)

Place the above copied folder under the EgretWinExample.Shared/js of VS project 

![](568a5ce0e2c9d.png)

Expand all the files

![](568a5ce0f10f1.png)

Will include the newly added folder into the project, namely, in the VS you can directly access 

![](568a5ce10ea36.png)

Open the configuration file

![](568a5cd2d99f7.png)

Modify the starting address according to the following level. Here it is fine to write in the starting file run in the egret project.

![](568a5cd3025b1.png)

![](568a5cd317280.png)

VS support two kinds of operation mode, one is Windows, the other is wphone.

![](568a5cd335b3e.png)

The running results of Windows. You can run with the wphone simulator.

![](568a5cd344e70.png)

### 5.3. Packaging

Before the start of the packaging, you need to provide the images required in the picture and modify the corresponding material address.In addition, because the publishing also needs images of other specifications

Logo: 71 * 71            150 * 150            310 * 150            44 * 44            58 * 58            120 * 120 300 * 300 //upload with 358 * 358//upload with 358 * 173 //upload with background image:             1152 * 1920 1000*800//Used for uploading

Game graph:     1280 * 768 or 7868 * 1280//used for uploading

![](568a5cd369c53.png)

Click Generate, then click on the app store -> create the application

![](568a5cd37f08f.png)

![](568a5cd39a795.png)

After you fill in the name in the application name, clicking Hold will be displayed in the above list

![](568a5cd403ef5.png)

![](568a5cd46914f.png)

![](568a5cd52ac6a.png)

Pack the generated files needed

![](568a5cd54f36e.png)

The following two steps are to test whether there is problem with the generated package. If yes, you need to solve the problem before repackaging.

![](568a5cd5b850c.png)

![](568a5cd5cdb3e.png)

### 5.4. Upload

Upload the packaged APP to WinPhone's official mall for uses to upload
    	    









