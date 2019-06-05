 DragonBones pro supports command-line import for batch processing starting at 4.3
`Import ( dbdata=""，texturefolder=""， textureatlas="xxx.png"， texturedata=""， dbdatapack=""， plugin="auto"， projectname=""， projectpath="" )`

import Command name:import
Parameter list:

|The parameter|Describes|
| ------------ | ------------ |
|dbdata|In a scatter or texture set project, import the data problem path for the project.|
|texturefolder|In the scatter plot project, the picture resource path.|
|textureatlas|Texture set project, texture set picture resource path.|
|texturedata|Texture set project, texture set data file resource path.|
|dbdatapack|zip Project, the resource path of the zip file.|
|plugin|[Optional parameter] is only available if the imported project is a scatter map project or texture set project.Used to specify the name of the plug-in to be used by the import.The default is auto, which will automatically select plug-in resolution based on actual data. If there is no plug-in name, DragonBonesPro will use its own engine resolution.|
|projectname|[Optional parameter] the name of the new project after import, which defaults to the name of the original data.|
|projectpath|[Optional parameter]the address of the new project after import, and the default is DBProjects folder under the user document directory.|

In the parameters shown in the above table, according to different import types, the required parameters to be filled in are different .

- Import the hash chart item：dbdata, texturefolder is a mandatory parameter
  For example： `DragonBonesPro import dbdata="C:\Demon.ExportJson" texturefolder="C:\texture" plugin="auto" projectname="new" projectpath="C:\ceshi"`
- Import texture set items：dbdata，textureatlas，texturedata is required
  For example： `DragonBonesPro import dbdata="C:\Demon.ExportJson" textureatlas="C:\Demon0.png" texturedata="C:\Demon0.plist" plugin="auto" projectname="new" projectpath="C:\ceshi"`
-  Import packet item: dbdatapack is required parameter
  For example： `DragonBonesPro import dbdatapack="C:\DragonOpening.zip" projectname="new" projectpath="C:\ceshi"`

Note: the above three import types are mutually exclusive, and parameters can only be entered according to one import type.