
## Introduction

ResDepot is the creation, editing and management tool for resource configuration files.You can use it to create resources' Jiugongge data. You can also enable such functions as grouping and publishing for the resources specified in the resource configuration file.Publishing is to map the resources within the resource configuration file and generate a new ResDepot file, so as to ensure that the number of resources can be reduced without changing the project code.

ResDepot is only a tool for resource management but it has no project concept itself. Its management unit is resource.json.

### Adapt to the platform

* Windows
* Mac OS X

### Adaptation version

* Egret Engine version 1.4.0 and above

### download link

* [Egret ResDepot download address] (http://www.egret.com/downloads/res.html)


## operation

### Open ResDepot

![image](1.png)

If the opened interface is empty. do not panic at this time.You can continue as follows:

* Create a new resource configuration file
* Open a resource configuration file.

### Load the resource

Here we choose to create and then continue to explain. Select all the resources under the directory CoreExample\resources\assets\480.Dragged into the following red frame.

![image](2.png)

So the resource was loaded.

![image](3.png)

### Create a group

![image](4.png)

Click the Add button in the resource group box, the following dialog box will pop up:

![image](5.png)

Here you can use the Enter key to confirm the creation.

### Add resources with the group

Select a group, hold down the ctrl to add more groups, or hold shift to multiselect the resources in the resource box, and then drag the resources to the red box.

![image](6.png)

The resource is added to the selected resource group.

![image](7.png)


### delete

Click on a selected resource or resource group, press the keyboard delete key to delete, then a dialog box pop up:

![image](8.png)

Here you can press the Enter key to quickly confirm.
This removal method applies to: deleting resources, deleting resource groups, and removing resources from within a group.


### Set relative path

![image](9.png)


Click on the browsing after the root path to select the root path of the project's resources.

![image](10.png)

All paths will automatically become relative paths.


> Absolute paths are used to generate relative paths and are not stored in the resource.json file, but are stored in ResDepot's own persistent location.So you only need to ensure that the relative path generated and others are consistent.

### Error and warning

It is possible that error may happen to the resource in the list. ResDepot has marked all resources with error for you.

Red represents error, that is, the duplicate name of the resource name, or duplicate name of resource group.Note that  the resource configuration file can never be saved in the case of errors.

Yellow indicates warning. For example, the correct resource file can't be put together according to the root directory, or there exist duplicate name within the sheet.The warning will not affect the preservation of the document, but will affect the visual editing of Jiugongge.

![image](11.png)

### Jiugongge editor

The Jiugongge of the image resource can be directly edited through the input on the form, or you can also enable the Jiugongge editor window to visualize the editor:

![image](12.png)

You can also directly enters through the preview button in the lower left corner of the preview:

![image](13.png)


After the operation is completed, there will be "Edit Jiugongge" menu, then click as shown below:

![image](14.png)

If you want to edit Jiugongge, you should first check the "open Jiugongge" check box on the upper left corner.Specifically, the editing method for the Jiugongge is as follows: (Note: the images can't be loaded until the root has been set correctly)

* Mouse wheel: zoom
* Drag the picture: Move the picture
* Drag the dotted line: edit Jiugongge

### Resource type settings

If you want to increase the file extension for a particular resource type, you can set it as follows: Settings -> Settings

![image](15.png)

Here, you can also add other types.You can also set the parsing rules for resource naming, as well as the file list that needs to be ignored.

### save

Click Save to automatically generate a json file in the selected directory.

### publish function

This feature is to customize a set of cohesive group, and then to combine the image resources in the `resource.json`, and then to generate the corresponding sheet file, and the new` resource.json`.
Publish function can combine the images based on the existing resources at the time of completing the project. It is different from TextureManager that is used during the process of developing project.ResDepot is used at the time when the project has been developed. Besides, the resource package from the ResDepot publishing is very negative for editing and development purpose. It is only designed to reduce the number of resources in the project and thus reduce the expense of the loaded io.Therefore, please be careful not to use the publish function during the project development process!

Instructions

![image](17.png)

As above.

We use GUIExample's resource_ocean.json as an example.

Open the resource_ocean.json with ResDepot. As shown below:

![image](17.png)


Now there are two resource groups, and then click the Publish button.

> You can not click the Publish button when there is no content in the group, or when there is an error).

![image](18.png)

Now there is no tool for combing images.We have to create a tool for combing images next, so that ResDepot can know which images can be combined into a sheet.

we can add a few groups by adding the button on the bottom right corner of the grouping area:

![image](19.png)


And then it prompts to drag the resource. At this moment you just need to select resources in the resources that haven't been grouped, and then drag the them to the specified group.As shown below:

![image](20.png)


When all the groups are filled,You can configure the combined image according to each group.

![image](22.png)


All changes to the configuration are saved in a configuration file of the combined image.There will be prompt that reminds you to save the configuration file of the combined image before publishing.


![image](22.png)

Here we explain the meaning of the several checked ones at the top of the publishing panel:

* Copy file that is referenced: Because some material may not be added to the resource.json, so check this incense will be based on the source directory. At the time of publishing, the resources that are not in the resource.json will be copied to the specified publishing directory.
* Empty the "publishing directory" when publishing: As we may publish for many times, checking this option can move the resources in the "publish directory" to the recycle bin before publishing.
* Add the CRC code to the file name: Sometimes after we have made changes, the contents of certain map may change, but the name has not changed. With this feature, the crc verification code of the file itself can be added to the end of the file name, but the key referenced by the generated resource.json for resource won't be changed.The is equivalent to the version control over your resources, so as to prevent the browser cache from causing resource reading errors.


> The combined image may not effectively reduce the volume of the image, but it can effectively reduce io overhead when the resource is loaded.

### search for

If there is any resources that can not be found, you can filter the search through filter.The tool will automatically filter out the resource entries that do not contain search keywords.

![image](23.png)

### shortcut key

For convenience, you can drag new resources directly into the resource group. At that moment, you can load the resources into resource.json wheelie adding the resources to the specified resource group.
Shortcut list:

* ctrl+n: create group
* ctrl+o: open a resource configuration json file
* ctrl+s: save the current editing
* ctrl+f: search
* delete: delete the resource, delete the resource group, remove the resources from the group
* Enter key: confirm various prompt box.

### Command line support

Added command line control in 1.4.1.

#### command

* -help This command allows ResDepot to pop up the help interface
* -pack [resource_path] [pack_config_path] [root_directory] package
    * resource_path The absolute path to the resource configuration file, such as the absolute path to resource.json.
    * pack_config_path The absolute path to the package configuration file, which can be edited and generated during manual packaging by ResDepot.
    * root_directory The resource's root directory, which is used to match with the relative path within the resource configuration to form an absolute path.


#### Usage

ResDepot's command line support is supported by the configuration file that needs to be packaged. However, the file can only be generated by ResDepot. So, if you want to ensure that the command line can be packaged successfully, first you are required to package successfully in the software.

Second, start the command line (Start the terminal under Mac).As shown below:

![image](24.png)

Packaging will be made according to packConfig.json if you press the Carriage Return key at this moment.