
## Introduction

Egret Inspector is a Chrome browser plugin.

Using the Inspector, you can penetrate the Canvas, position the display object directly with the mouse, and the Inspector will highlight the border and coordinate of the object.The display list panel will display the level of the currently selected object, which is clear at a glance. As a result, UI debug efficiency is significantly improved.The property panel will display all attribute values of the currently selected object, further facilitating debugging. You can also directly modify the attribute and view the effect after modifications in a real-time manner.

### Adapt to the platform

* Windows Chrome 30 or later
* Mac OS X Chrome 30 or later

### Adaptation version

* Egret Engine 2.5.4 version and later

### Download link

* [Egret Inspector download address](http://www.egret.com/downloads/inspector.html)

## Installation Instructions

* Download Egret Inspector: [Download address](http://www.egret.com/downloads/inspector.html)
* Open Chrome and go to the Chrome extension tool page (you can directly open by directly typing chrome: //extensions/).
* Drag the downloaded crx file into Chrome's Extensions tool window

	![image](1.png)


* Click OK to install

	![image](2.png)

* The state of completed state:

	![image](3.png)

> To ensure that the tool is available, please restart the browser

## Instructions for use

1. With Chrome, open the items that need to be checked, and open Chrome developer tools

	![image](4.png)

2. Open the Egret Inspector by clicking on the Egret button on the panel 

	![image](5.png)


3. When mouse clicks on the elements in the game scene, the element will be highlighted in the scene, while the Inspector will display the display list tree in the current scene.

	![image](6.png)

## Panel details

### FPS display

![image](8.png)

### Display the list panel

![image](9.png)

* Prevent clicking events

When you want to check the objects that will disappear after clicking buttons and others, please check the "prevent clicking action" option and then check the operation.

![image](14.png)


* Show the object swept by the mouse 

Check the "Highlight sweeps the object" option in the display list panel, and then highlight the objects swept by the mouse when the mouse moves in the scene

![image](11.png)


* Select the clicked object

Highlight the object clicked by the mouse and display the attributes of the object in the Attribute panel.When you cancel this option, the mouse click action will no longer be tracked

![image](22.png)


* Refresh button

Since the display list tree changes frequently in the game, the display list tree in the Inspector is not updated in real time, instead, it is updated when the mouse clicks on the object.When you do not click for a long time, the display list tree may not be automatically updated due to great differences between it and the structure in the scene. Then you can click the Refresh button and begin reloading the display list tree.

![image](13.png)


* Expand the display list

In the real list tree, if there is + symbol in front of the object, it indicates that the object contains child elements, you can click to expand. The check box behind the display object is to quickly hide or display the object's switch, making it convenient to easily view the covered object

![image](15.png)


* Search in the search box under the actual list tree (shortcut Ctrl/Command + Shift + F) by entering the display object name or hashCode

* Store global objects
Right click on the object in the display list and click Save as Global Variable. The global variable name and the object will be exported in the console

### Attribute panel

![image](10.png)

* Option switch

	![image](21.png)

	* List the method:：
The method is displayed in the attribute list, and the contents of the method are displayed when the mouse passes

	![image](17.png)

	* List the private attribute:
Select whether to display the attributes that begin with an underscore, not TS's private

	![image](18.png)

* Attribute editing
	By double clicking on the attribute value, you can edit the attribute, enter or leave the input box to submit the changes

	![image](19.png)

	For a attribute that only provides Getter rather than Setter method, it can not be edited
	![image](20.png)


* Search for the attribute or the attribute value in the search box under the attribute list (shortcut Ctrl/Command + F) by entering character

* Store global objects
Right click on the item in the attribute list and click Save as Global Variable. The global variable name and the object will be exported in the console
