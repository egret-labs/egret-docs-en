# Summary
The plug-in specification is opened and the management of import plug-in is realized. The purpose is to make it convenient for users to import animation data in any format into DragbonesPro for secondary editing through the plug-in，Animation in DragonBones format is generated to run animation in any engine supporting DragonBones, including Egret.This article covers the basic specification for writing plug-ins and how to write an import plug-in for DragonBones in the current release.

# Plug-in naming conventions
Plug-in unified extension expl, is essentially a zip package, internal at least need to contain *.excfg, *.png, *.js, 3 files. Among them:
- *.excfg is the plugin configuration file for json format.。
- *.png is the icon for the plug-in, and the standard size is 32x32.
- *.js is the main script file for the plug-in. Content standards for js scripts may vary depending on the type of plug-in. For example, the import plug-in of DBPro needs to inherit the DBImportTemplate class in egretpluginsdk.js, and rewrite all methods.The js file is the main script file for the plug-in. Content standards for js scripts may vary depending on the type of plug-in. For example, the import plug-in of DBPro needs to inherit the DBImportTemplate class in egretpluginsdk.js, and rewrite all methods.（Note：egretPluginSdk is a framework for writing extendable plug-ins in the egret toolchain. At present, it only contains the basic classes and methods required by DBPro import plug-ins. egretPluginSdk.js  in the plugins directory of DragonBonesPro installation directory）

#### Plug-in authoring specification
The *.excfg file format is specified as follows, for example:the Spine plug-in
``` TypeScript
{
    "name":"Spine 2.x Importer", //Plug-in name
    "path":["spine.js"],//The main script for the plug-in and the containing script
    "description":"Spine 2.x Importer can import Spine 2.x animation data to DragonBonesPro",//Description of the plug-in
    "author":"Egret Engine",//Plugin developer
    "version":"1.0.0",//The version number of the plug-in
    "icon":"icon.png"//Plug-in icon(32*32)
}
```

The *.js file format is as follows. For example, when importing plug-ins, the egretpluginsdk. js was inheritedDBImportTemplate class。The DBImportTemplate  class format is as follows:

``` TypeScript
var DBImportTemplate = (function () {
    function DBImportTemplate() {
        this._type = "DBImportTemplate";
    }
    /**Supports the extension of the imported data file**/
    DBImportTemplate.prototype.dataFileExtension = function () {
        return ["*"];
    };
    /**Supports the description of imported data files**/
    DBImportTemplate.prototype.dataFileDescription = function () {
        return "";
    };
    /**Texture set data file extension**/
    DBImportTemplate.prototype.textureAtlasDataFileExtension = function () {
        return ["*"];
    };
    /**Checks whether the imported data supports the texture set**/
    DBImportTemplate.prototype.isSupportTextureAtlas = function () {
        return false;
    };
    /**Verify that the imported data supports this parser**/
    DBImportTemplate.prototype.checkDataValid = function (data) {
        return true;
    };
    /**Parsing of imported data**/
    DBImportTemplate.prototype.convertToDBData = function (data) {
        return data;
    };
    /**Parsing of texture sets**/
    DBImportTemplate.prototype.convertToDBTextureAtlasData = function (data) {
        return data;
    };
    DBImportTemplate.prototype.type = function () {
        return this._type;
    };
    return DBImportTemplate;
})();
```

Note that the entry class of *.js must be named main. For example, the Spine data import plug-in may be listed as follows:
``` TypeScript
var __extends = (this && this.__extends) || function (d, b) {
    for (var p in b) if (b.hasOwnProperty(p)) d[p] = b[p];
    function __() { this.constructor = d; }
    __.prototype = b.prototype;
    d.prototype = new __();
};
var main = (function (_super) {
    __extends(main, _super);
    function main() {
        _super.apply(this, arguments);       
    }
    main.prototype.dataFileExtension = function () {
        return ["Json"];
    };
    main.prototype.dataFileDescription = function () {
        return "Spine data";
    };
    main.prototype.textureAtlasDataFileExtension = function () {
        return ["atlas", "texture"];
    };
    main.prototype.isSupportTextureAtlas = function () {
        return true;
    };
    main.prototype.convertToDBTextureAtlasData = function (data) {
        var dbTexture = {};
        return JSON.stringify(dbTexture);
    };
    main.prototype.checkDataValid = function (spineJson) {
        return false;
    };
    main.prototype.convertToDBData = function (spineJson) {
        var DBJson = {};
        try {
          ...
        }
        catch (e) {
        }
        return JSON.stringify(DBJson);
    };
    return main;
})(DBImportTemplate);
```
Note: to ensure the security of the plug-in, the developer must add a try catch to the code.

Finally, the two plug-ins that come with DragonBonesPro are in the plugins folder of the installation directory, and "Cocos 1.x Importer. Expl" and "Spine 2.x Importer. Expl" can be used as a complete example for reference.

# Installation and use of plug-ins:
The current way to install DragonBonesPro plugins is to open the plugins administration panel under the help menu, click on the top right corner to install plugins, and select files in expl format to complete the installation. Subsequent versions will support double - click installation.