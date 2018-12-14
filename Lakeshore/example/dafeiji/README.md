##  Create a Game Project

Open Lakeshore and click the menu "file", "new project",Enter the name and size of the game and click ok.The newly created game project automatically creates a scene and corresponding event table. As shown in the figure below:

![](56b1cbc771383.png)

## Import Picture Material

In the project panel, right-click the "pictures" folder and click "add picture materials".Select the image you want to import in the file selection dialog box that pops up. As shown in the figure below:

![](56b1cbc79d210.png)

Click the imported image in the project panel to directly preview the content and size of the image. As shown in the figure below:

![](56b1cbc7c66d2.png)

## Add Sprites to the Scene

Select a background resource under the images folder in project and drag it into the scene.Create a wizard, in the right property bar to set its name called "scroll background", and set other properties, as shown in the figure below:

![](56b1cbc83fa34.png)

## Add the Behavior

Click the "add behavior" button in the behavior list at the bottom of the property bar to bring up the "behavior list" property box.Double-click and select "scroll behavior" to bind "scroll behavior" to "scroll background", as shown in the figure below:

![](56b1cbc85e2ff.png)

After binding the scrolling behavior, we set its scrolling direction downward in the behavior list, as shown in the figure below:

![](56b1cbc8ccc43.png)

In general, in order to achieve seamless scrolling, you need two images that can be seamlessly connected back and forth or up and down.So this is a very special material, it's seamlessly connected up and down, so if I hold Ctrl,Drag the mouse to "scroll background" to "duplicate" scroll background "and set the basic properties of" scroll background "to be copied, as shown in the figure below:

![](56b1cbc9a5ead.png)

If you look at the two pictures above, you can see that,The scroll background in the first picture, the y-coordinate is -768, and the scroll background in the first picture is connected,In addition, after copying, the original image has the same name as the copied image, and if scrolling behavior is added to the original image, then scrolling behavior is added to the copied image.

Click the Lakeshore menu bar "file" - "run" to preview in the default browser (chrome as an example).In the preview, you will find that the background has been able to achieve seamless scrolling, as shown in the figure below:

![](56b1cbcbace32.png)

## Add Red Fighter

Hold down the red fighter in the image folder of the project panel and drag it into the scene.Select the "red fighter" spirit,You can drag and drop control points on the Sprite to adjust the Sprite position and rotation Angle.Name the Sprite "red fighter" in the right property bar, as shown in the figure below:

![](56b1cbcd2597d.png)

## Add the Behavior

Select the current "red fighter" and click "add behavior" in the behavior list at the bottom of the property bar.Here we can double click on the "drag and drop behavior" to bind the "drag and drop behavior" to the aircraft.After the drag-and-drop behavior is added, the aircraft can drag and drop on the phone, as shown in the figure below:

![](56b1cbcd81ff9.png)

Then, click the Lakeshore menu bar "file" - "run" preview,Press and hold the mouse "red fighter" drag can be tested. As shown in the figure below:

![](56b1cbd016d14.png)

## Add a Bullet

Follow the steps to add the red fighter, select a bullet material, and drag it onto the stage.Name it "red fighter bullet" in the base properties bar.Follow the "add action" operation to add "bullet action" and "destroy the border" to the wizard.And in the "action list" to set the bullet behavior parameters "set the Angle" to "no", other default. As shown in the figure below:

![](56b1cbd27af47.png)

## Add Event

In order for the red fighter to fire bullets, therefore, we need events to correlate them.Double-click the event table "MainSceneEventSheet" in the "project" column, and create the "red fighter launched bullets event" in the event table, as shown in the figure below:

![](56b1cbd2f328e.png)

## Add the Condition

In order for the red fighter to continue firing bullets, we need to add conditions.For example, launch one bullet in 0.1 seconds. Select "red fighter launches bullet event" and click "add condition" under the condition bar on the right side of the panel.Select "System" in the pop-up conditional target panel, as shown in the figure below:

![](56b1cbd37217c.png)

Then select "execute once every few seconds" from "conditional list", as shown in the figure below:

![](56b1cbd4546c5.png)

In the popup property setting panel, the time interval is set to 0.1, that is, 10 bullets are fired in 1 second, as shown in the figure below:

![](56b1cbd4b93d1.png)

## Add the Action

Notice that this time is in seconds, and once you've set the conditions, you need to set the actions,The action here is to create bullets in the position of "red fighter". Click "add action" under the condition bar on the right side of the panel.Select "red fighter" in the action target panel that pops up, as shown in the figure below:

![](56b1cbd4eeca9.png)

Double-click "red fighter", and the "action list" pops up. Select "manufacture" in the action list, as shown in the figure below:

![](56b1cbd5492a7.png)

Double-click the "make" action and select "red fighter bullet" in the manufacturing properties panel that pops up.And set its vertical offset value to -80. Note that "horizontal offset" and "vertical offset" are relative coordinates.That is, the coordinates relative to the red fighter are in pixels, as shown in the figure below:

![](56b1cbd63800f.png)

Click the Lakeshore menu bar "file" - "run" to preview,That is, you can see the continuous firing of bullets from the red warplane. As shown in the figure below:

![](56b1cbd807974.png)

Figure 26 shows that the bullet was fired horizontally, because we did not set the Angle at which the bullet was fired.We need to add the action of setting Angle, click "add action", and the action target selection dialog box will pop up, and select "red fighter bullet", as shown in the figure below:

![](56b1cc3ad94ae.png)

Double-click "red fighter bullet" to pop up the action list dialog box, and select "set Angle" in the action list, as shown in the figure below:

![](56b1cc3b14404.png)

Double-click "set Angle", and the setting Angle property panel pops up. Change the Angle to -90 degrees, that is, the direction is upward, as shown in the figure below:

![](56b1cc3b3bdfd.png)

Click the Lakeshore menu bar "file" - "run" to preview and see that the bullet has been fired upward in the correct direction. As shown in the figure below:

![](56b1cc3c241db.png)

## Add Enemy and Enemy Bullets

According to the operation method of "red fighter" and "red fighter bullet",We added "enemy fighter" and "enemy fighter bullet" respectively and set "bullet" behavior and "out of bounds destruction" behavior for them (note: "out of bounds destruction" behavior helps improve game performance and avoid memory leakage).And set the "enemy fighter" behavior list "set the Angle" to "yes", the Angle is 90 degrees, make it face down,Also, set the "set Angle" in the "enemy fighter bullet" action list to be yes and the Angle to be 90 degrees. That is, the movement direction of "enemy fighter" and "enemy fighter bullet" is downward, as shown in the figure below:

![](56b1cc3cad2d4.png)

Also add events to MainSceneEventSheet so that the enemy can fire enemy bullets，"Enemy fighter fires enemy bullets", and add the condition "once every 0.2 seconds" to the event, and the action "fire enemy fighter bullets", as shown in the figure below:

![](56b1cc3e463cd.png)

Click the Lakeshore menu bar "file" - "run" to preview, and you will see the following figure:

![](56b1cc3f9c005.png)

In order for "enemy fighters" to be hit by our "red fighter bullets" and cause damage calculations,So, we need to set "participate in collision" as yes for "enemy fighter" and "red fighter bullet" as yes and select "enemy fighter".In the other property bar on the right side of the panel, set "yes" to participate in the collision, and the same is true for "red fighter bullet", as shown in the figure below:

![](56b1cc409675d.png)

In order to give "enemy fighter" life, we add custom attribute HP to "enemy fighter".Select "enemy aircraft", click "add properties" in the property bar "custom properties", and pop up the custom properties dialog box.Set the property name to: HP, the value type to: number, and the value to 10, i.e., "enemy fighter" has an initial 10 HP. As shown in the figure below:

![](56b1cc422ab13.png)

In order to reduce the HP of the "enemy fighter" when the "red fighter bullet" hits the "enemy fighter", that is, the HP of the "enemy fighter" is reduced by 1 per collision.Then, we need to create a new event "red fighter bullets hit enemy fighter blood loss event", and add conditions, as shown in the figure below:

![](56b1cc4284d2f.png)

Double-click "red fighter bullet" and select "collision" in the pop-up condition list, as shown in the figure below:

![](56b1cc43aa9db.png)

Double-click "collision" and select "enemy aircraft" in the collision properties dialog box, as shown in the figure below:

![](56b1cc4414cab.png)

At this point, we add actions to make the enemy aircraft HP minus 1, as shown in the figure below:

![](56b1cc44b181d.png)

Double-click "subtraction operation", select the custom property HP in the "subtraction operation" property box, and set the value to 1, as shown in the figure below:

![](56b1cc454b220.png)

So far, "red fighter bullet" will lose blood if it encounters "enemy fighter".However, in order to be able to preview the actual effect, we also need to add the event "destruction event after enemy fighter's blood volume is less than or equal to zero".And add conditions: if "enemy fighter" HP is less than or equal to 0, as shown in the figure below:

![](56b1cc45c0df4.png)

Double-click "compare instance variables", and in the properties dialog box that pops up, set the instance variable to HP, the operator to be less than or equal to, and the value to be 0, as shown in the figure below:
![](56b1cc462801a.png)

And add the action "destroy", first select "enemy aircraft", as shown in the figure below:

![](56b1cc466b81d.png)

Double-click "red fighter" and select "destroy", as shown in the figure below:

![](56b1cc46d51cc.png)

At this point, the "enemy fighter" is destroyed when the HP of the enemy fighter is less than or equal to 0, as shown in the figure below:

![](56b1cc4814e44.png)

Preview we found that "red fighter bullet" will penetrate "enemy fighter",At this point, we need to add a "red fighter bullet" encounter "enemy aircraft" destruction action,Select the event "red fighter bullets hit enemy fighter blood loss event" and click "add action".In the action target panel, double-click to select "red fighter bullet" and add "destroy" action.Preview effect, found that "red fighter bullet" hit "enemy fighter" will not penetrate, as shown in the figure below:

![](56b1cc4a32bbb.png)

In general, fighter games have a steady stream of enemies.So we need to create a constant stream of enemy events here,Event name: create 1 enemy event every 2 seconds in the scene, add conditions as described above: execute once every 2 seconds, then add actions, click "add actions", double-click "System", and select "create object", as shown in the figure below:

![](56b1cc5bcf1d1.png)

Double-click "create object" and select the object type as "enemy fighter" in the pop-up create object property panel.Enter math.random ()*500 in the horizontal coordinate and math.random ()*200 in the vertical coordinate to represent the position of the enemy fighter plane created between the horizontal coordinate 0~500 and the vertical coordinate 0~200, as shown in the following figure:

![](56b1cc5c22241.png)

Preview, found every 2 seconds to create an "enemy aircraft", as shown in the figure below:

![](56b1cc5d3d891.png)

At this point, the game Demo is finished, but in order to play the performance and memory of the game, we need to add "out of the boundary destruction behavior" to "red fighter bullet", "enemy bullet" and "enemy fighter".

Finally, we can publish the game we have finished. Select "file" - "publish" to publish our game.A dialog box will pop up to remind us to save the path of our published game, as shown in the figure below:

![](56b1cc5e2fc10.png)

