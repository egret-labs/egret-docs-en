Usage: egret `command` [-v]

command list:

## create
Create a new project

### Usage:

    egret create project_name [--type empty|game|gui|eui]
### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` | The project name, which is named according to the naming convention of the operating system
| `- type` | The type of project to be created: empty, game, gui and eui. The default is game


### example:

    1. Create an eui project named [HelloWorld]
    egret create HelloWorld --type eui
    2. Create an empty project named [HelloWorld]
    egret create HelloWorld --type empty

## create_lib
Create a new third-party library project

### Usage:

    egret create_lib lib_name
### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `lib_name` |    third-party library name, which is named according to the naming convention of the operating system




## create_app
Generate app from h5 game

### Usage:

    egret create_app app_name -f h5_game_path -t template_path

### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `app_name` |    Mobile app project name, which is named according to the operating system naming convention
| `-f` |          app project corresponds to the path to h5 project
| `-t` |          corresponds to the Native Support path

    If it is compiled under the project folder, do not add the project name
    Note: it's better to add quotation marks to the path, thus preventing blank error in the path

## build
Build the specified project

### Usage:

    egret build [project_name] [-e] [--runtime native]
### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` | The project name, which is named according to the naming convention of the operating system
| `-e` |              compile the specified project while compiling the engine directory
| `--runtime` |       If there is a native project, the file will be copied to the project

    If it is compiled under the project folder, do not add the project name


### example:

    1. compile【HelloWorld】
    egret build HelloWorld
    2. compile [HelloWorld] while compiling engine
    egret build HelloWorld -e
    3. compile [HelloWorld] whiling compiling the native project
    egret build HelloWorld --runtime native

## publish
Publish the project

### Usage:

    egret publish [project_name] [--version [version]] [--runtime html5|native] [--passWorld]

### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` |       The project name, which is named according to the naming convention of the operating system
| `--version` |       Set the version number after publishing. It's fine not to set
| `- runtime` |       Set the publishing method as html5 or native, and the default value is html5
| `--password` |     Set the decompression password for publishing zip file

    If it is compiled under the project folder, do not add the project name

### example:

    Publish【HelloWorld】
    egret publish HelloWorld --version 0.03 --passWorld 88888888

## startserver
Start HttpServer and run the specified project in the default browser

### Usage:

    egret startserver [project_name] [--port 3000] [-ip] [-serveronly]
### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` |       The project name, which is named according to the naming convention of the operating system
| `--port` |          Specify the port number
| `-ip` |             Whether to use native IP
| `-serveronly` |     Whether to run only the server

    If it is compiled under the project folder, do not add the project name

### example:

    Run the [HelloWorld] project
    egret startserver HelloWorld --port 3000

## clean
Reset the engine code in the project

### Usage:

    egret clean [project_name]
### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` |       The project name, which is named according to the naming convention of the operating system

    If it is compiled under the project folder, do not add the project name

## upgrade
Upgrade the project code along with the upgrade of the Egret engine 

### Usage:

    egret upgrade [project_name]
### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` |       The project name, which is named according to the naming convention of the operating system

    If it is compiled under the project folder, do not add the project name

### example:

    Upgrade the【HelloWorld】project
    egret upgrade HelloWorld

## make
After modifying the engine source code, compile the engine source

### Usage:
    egret make

## apitest
After the version is upgraded, detect whether the api has been replaced or not.It is limited to the detect of upgrade from pre-2.4 version 2.5 (and above), and you need to enter in version 2.5 (and above)

### Usage:

    egret apitest [project_name]

### Parameter Description:

| Keywords | description
| ------------ | ------------ 
| `project_name` |       The project name, which is named according to the naming convention of the operating system


### example:

    Detect whether there is a conflict with the [HelloWorld] project api
    egret apitest HelloWorld

## info
Get Egret information, such as the current Egret version and the installation path

### Usage:

    egret info

## help
Understand the details of each command

### usage
    egret help `command`
