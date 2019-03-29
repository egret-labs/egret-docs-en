
# Usage
`egret [command]`
### For example：
	1、Run a project called HelloWorld
	egret run HelloWorld
	2、Compile a project called HelloWorld
	egret build HelloWorld

# The command list:

## Create
Create a new project

### Usage:

    egret create project_name [--type core|eui]
### Parameter description:

| keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system
| `--type` |          The project type to be created, either core or eui, has a default value of core


###  For example:
	1、Create an empty project named HelloWorld
	egret create HelloWorld
	2、 Create a eui project named HelloWorld
	egret create HelloWorld --type eui


## Create_lib
Create a new third-party library project

### Usage:

    egret create_lib lib_name
### Parameter description:

| keyword | description
| ------------ | ------------ 
| `lib_name` |    Third party library name, according to the operating system naming specifications




## Create_app
Generate app from h5 game

### Usage:

    egret create_app app_name -f h5_game_path -t template_path

###  Parameter description:

| keyword | description
| ------------ | ------------ 
| `app_name` |    Mobile application project name, according to the operating system naming specifications
| `-f` |          The path of the h5 project corresponding to the app project
| `-t` |          Corresponding to the Native Support path

    If you are compiling under a project folder, do not add a project name
    Note: the path is best in quotation marks, to prevent the path has a space error

## Build
Build the specified project

### Usage:

    egret build [project_name] [-e] [--target wxgame|bricks|ios|android]
### Parameter description:

| keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system
| `-e` |              Compiles the engine directory while compiling the specified project
| `--target` |       编Compile the target version, optional parameters have  `wxgame`：WeChat little game;`bricks`：play; `android`：android projects；`iOS`：iOS projects.

	 If the command is executed under the project folder, the project name can be omitted


### For example:

    1、Compile 【HelloWorld】
    egret build HelloWorld
    2、Compile the【HelloWorld】engine at the same time
    egret build HelloWorld -e
    3、Compiled WeChat small game project while compiling 【HelloWorld】
    egret build HelloWorld --target wxgame

## Publish
Publish projects

### Usage:

    egret publish [project_name] [--version [version]] [--target wxgame|bricks|ios|android]
### Parameter description:

| keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system
| `--version` |        Set the version number after the release, you can not set
| `--target` |       Compile the target version, optional parameters have  `wxgame`：WeChat little game；`bricks`：play；`android`：Android projects；`iOS`：iOS projects.

    If the command is executed under the project folder, the project name can be omitted

### For example:

    Release 【HelloWorld】 to WeChat mini-game
    egret publish HelloWorld --version 0.03 --target wxgame

## Run
Start the local server and run the specified project in the default browser

### Usage:

    egret run [project_name] [--port 3000] 
### Parameter description:

|  keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system
| `--port` |          Specify port number


    If the command is executed under the project folder, the project name can be omitted

### For example:

    Run the [HelloWorld] project on the specified port
    egret startserver HelloWorld --port 3002

## Clean
Reset the engine code in the project

### Usage:

    egret clean [project_name]
### Parameter description:

| keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system

     If the command is executed under the project folder, the project name can be omitted

## Upgrade
Upgrade project code

### Upgrade after Egret Launcher v1.0

#### Usage:

    egret upgrade [project_name] --egretversion [target version]
#### Parameter description:

| keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system
| `target version` |   The target version number to switch

    If the command is executed under the project folder, the project name can be omitted

#### For example:

    Upgrade the current directory to 5.1.0
    egret upgrade --egretversion 5.1.0

### Upgrade before Egret Launcher v1.0

#### Usage:

    egret upgrade [project_name]
#### Parameter description:

| keyword | description
| ------------ | ------------ 
| `project_name` |    Project name, named according to the naming conventions of the operating system

    If the command is executed under the project folder, the project name can be omitted

#### For example:

    Upgrade 【HelloWorld】 porjects
    egret upgrade HelloWorld

###  Introduction to the Egret Launcher v1.0 version of the project

    1. Modify the version number under the field 'egret_version' in the configuration file 'egretProperties. Json 'in the project root directory
    2. Implement egret clean and reduce the project to the target version

## Make
After modifying the engine source code, compile the engine source code. If there are no special requirements, it is not recommended for ordinary users

### Usage:
    egret make



## info
 Obtain Egret information, such as the current Egret version, and the installation path

### Usage:

    egret info

## Help
Learn the details of each command

### Usage
    egret help [command]
