Here's a simple easing animation to show you how to use animation.

![](http://xzper.qiniudn.com/2016/12/animation/17.gif)

### 1. Create EUI projects and skin files

Select an Egret EUI project from the Project Creation Wizard.

Create a skin file for AnimationSkin.exml. Set the skin class name as "skins.AnimationSkin"

![](http://xzper.qiniudn.com/2016/12/animation/18.png)

In the ** design mode**, add a new button by dragging and dropping it to the skin file.

![](http://xzper.qiniudn.com/2016/12/animation/01.png)

Since the animation involves changing the rotation attributes of the component, it is recommended that the anchor point is set to the center, set the width and height of the button, and the anchor point property.

![](http://xzper.qiniudn.com/2016/12/animation/19.png)


**TIPS:** Try not to set the automatic layout (left, right, top, bottom, horizontalCenter, verticalCenter) attributes for the target object to which you want to add an animation. These attributes may make the x, y, widht, height attributes of the object invalid. If the animation involves the values that change these attributes, then the performance of the animation will be abnormal.


### 2. Switch to animation mode

Switch to the animation mode. In the animation mode, the following Panel panel will be added with an animation panel.

![](http://xzper.qiniudn.com/2016/12/animation/03.png)

Please remember this important panel because animation adding, editing and previewing will be done on this panel.

**TIPS:** Some behaviors will be disabled or restricted in animated mode. For example, in the animation mode, you can not delete/copy/paste the display object, and the corresponding shortcut will be invalid. In the ** non-critical frame state**, you also can not set such attributes as location and size of the display object. If you want to operate the display object, please **switch to the design mode** or **operate the attributes in the key frame**.


### 3. Add animation groups and animations

The animation is played in **groups**, and each animation group can set the animation attributes for **multiple display objects**.

First, use the '+' button in the lower left corner of the animation panel to add an animation group, then set the animation group id, where id is set as tweenGroup.

![](http://xzper.qiniudn.com/2016/12/animation/04.png)

Next, add the first animation to the animation group. But you can find Add button in the animation column of is gray and not available. Before you add an animation, you need to select a display object and specify the corresponding animation target. 

Here, taking the newly added button as an example, first select the button in the editing area.

![](http://xzper.qiniudn.com/2016/12/animation/05.png)

At this point,  the Add button on the animation column of the animation panel can be operated.

![](http://xzper.qiniudn.com/2016/12/animation/06.png)

Clicking the Add button to add an animation to the object.

![](http://xzper.qiniudn.com/2016/12/animation/07.png)

"Button" is the id of the button. If the target object does not set the id attribute, one will be created automatically, otherwise the user id set by the user will be used. 

### 4. Edit the animation attributes

Each animation corresponds to an animation timeline. The attribute of the target object at different time can be changed by adding **keyframes** and **easing behavior** to the timeline. At this point, there is no keyframe and animation behavior on the timeline.

![](http://xzper.qiniudn.com/2016/12/animation/08.png)

#### Add keyframes

First, right click on the position of 1s of the timeline to select the "Add keyframe".

![](http://xzper.qiniudn.com/2016/12/animation/09.png)

When it is added, the timeline will use "■" symbol to indicate that this is a keyframe.

![](http://xzper.qiniudn.com/2016/12/animation/10.png)

In the location of the keyframe,  such attributes as object's size, location, zoom, rotation and transparency can be set. Similar to the design pattern, you can **operate the display object** or set the keyframe attributes in the **Attributes panel on the right.**

![](http://xzper.qiniudn.com/2016/12/animation/11.png)

Here we set Y, zoom, transparency, rotation, easing function and other attributes according to the state of the animation at the moment. Note: If the attributes of the keyframe are not filled in, it indicates that the attribute won't be changed.

![](http://xzper.qiniudn.com/2016/12/animation/12.png)

#### Create tween animation

Only the key frame is not enough. The animation in the key frame will be the target attribute will be set as the value of the key frame. If you want the target object to "move", you need to add a tweened animation.

Right-click on the location of the keyframe or at any previous time to select "Create Tween Animation".

![](http://xzper.qiniudn.com/2016/12/animation/13.png)

The timeline will use "●" to mark the beginning and end of the tweened animation, and the "→" mark is a tweened animation.

![](http://xzper.qiniudn.com/2016/12/animation/14.png)

Since there are no other keyframes before adding the position of the tweened animation, the beginning of the segment tween is the beginning of the 0 position.

This creates a 1-second tweened animation that continuously sets the object's attributes so that it will move.

#### Modify keyframe position and tween animation time

If you want to change the start position or duration of a keyframe or tweened animation, you can drag the keyframe position directly on the timeline.

![](http://xzper.qiniudn.com/2016/12/animation/15.gif)

### 5. Preview the animation

After the animation editing is completed, you can preview the animation by **dragging the timestamp on the timeline** or **by clicking the play button below the timeline**.

![](http://xzper.qiniudn.com/2016/12/animation/16.png)

### 6. Call in code

The final skin file:

AnimationSkin.exml

    <?xml version="1.0" encoding="utf-8"?>
	<e:Skin class="skins.AnimationSkin" width="400" height="300" xmlns:e="http://ns.egret.com/eui" xmlns:w="http://ns.egret.com/wing" xmlns:tween="egret.tween.*">
		<w:Declarations>
			<tween:TweenGroup id="tweenGroup">
				<tween:TweenItem target="{button}">
					<tween:Wait duration="500"/>
					<tween:To duration="500">
						<tween:props>
							<e:Object y="{200}" scaleX="{1.5}" scaleY="{1.5}" rotation="{180}" alpha="{0.5}"/>
						</tween:props>
					</tween:To>
				</tween:TweenItem>
			</tween:TweenGroup>
		</w:Declarations>
		<e:Button id="button" label="按钮" x="193" y="35" width="100" height="50" anchorOffsetX="50" anchorOffsetY="25"/>
	</e:Skin>
		<e:Button id="button" label="按钮" x="193" y="35" width="100" height="50" anchorOffsetX="50" anchorOffsetY="25"/>
	</e:Skin>
In the project, through the following code, the user can play the animation in the animation group animation when clicking the button:

AnimationPanel.ts

	class AnimationPanel extends eui.Component {
		constructor() {
			super();
			// set the skin of the current panel
			this.skinName = skins.AnimationSkin;
		}
	
		/**
		 * The corresponding id in EXML is the animation group object in tweenGroup
		 */
		public tweenGroup: egret.tween.TweenGroup;
	
		/**
		 * The corresponding id in EXML is the button object of button
		 */
		public button: eui.Button;
	
		/**
		 * Animation group playback is completed
		 */
		private onTweenGroupComplete(): void {
			console.log('TweenGroup play completed.');
		}
	
		/**
		 * One of the animation groups is played
		 */
		private onTweenItemComplete(event: egret.Event): void {
			const item = event.data as egret.tween.TweenItem;
			console.log(item.target);
			console.log('TweenItem play completed.');
		}
	
		/**
		 * Play the animation when the button is clicked
		 */
		private onButtonClick(): void {
			this.tweenGroup.play();
			//this.tweenGroup.play(0); play from the beginning
		}
	
		protected createChildren(): void {
			super.createChildren();
			this.tweenGroup.addEventListener('complete', this.onTweenGroupComplete, this);
			this.tweenGroup.addEventListener('itemComplete', this.onTweenItemComplete, this);
			this.button.addEventListener(egret.TouchEvent.TOUCH_TAP, this.onButtonClick, this);
		}
	}


Finally, if you are interested in the realization of the animation, please study the animation part in the EXML, and the source code for realizing the animation can be found in the GitHub:

https://github.com/egret-labs/egret-core/blob/master/src/extension/tween/TweenWrapper.ts

