![](564ad9fa78d4b.png)

The text component is used to display text, and support static and dynamic text display, also can be set as inputable text field.
- Static text inherent text of the content, and the content won’t be changed in game, such as story plot introduction.
- The content of dynamic content will change according to game progress, such as score and HP volume.
- The inputable text field is a text box that’s provided to players for content input in game.

### Unique Properties
![](564ad9fa4164f.png)
- Default text: set the default display text of text field. (Only static text is supported, expression is not. if you want to implement dynamic text display, you need to do some setting in text action.)
- Font: set default font for text. The default value is “Song”.
- Font size: set font size of text. The default value is 12.
- Font color: set text color. The default value is white.
- Bold: set if text is bold or not. the default value is “bold”.
- Input enabled: set inputable text field enabled or not. the default value is “disabled”.
- Horizontal layout: set horizontal alignment type of text. The default value is “horizontal center” and the options are:
 - left alignment
 - right alignment
 - horizontal center
- Vertical layout: set the vertical alignment of text. The default value is “vertical center”, and the options are:
 - upper alignment
 - lower alignment
 - vertical center
- Upper limit of characters：Set the upper limit of characters number display in text field. The default value is 100.
- Italic: set if the text is italic or not. the default value is “no”.
- Password display: set if display as password form or not. the default value is “No”.
- Line break support: set if it supports line break or not. The default value is “No”.

*Note: The text does not support collisions.

------------


### Text conditions
In addition to the unique conditions, the text component also applies some general conditions (the related conditions of the text does not support “collision”). Please refer to: [general conditions](../../../../Lakeshore/manual/commonElements/conditions/README.md)

![](564ad9fa5cfc5.png)
#### Text content comparison
If the text content of text field is same with the specified text content.[continuous trigger]
Text content comparison, if they are same then the condition is true, and will continuously trigger action.
![](564ad9fa66759.png)

------------


### Text actions
In addition to the unique actions, the text component also applies some general actions (the related actions of the text does not support “collision”) please refer to:[general actions](../../../../Lakeshore/manual/commonElements/action/README.md)

![](564ad9f917a87.png)
#### Text content
Set the text display content. You can use expressions, and can set dynamic text based on it.
![](564ad9f99f3d2.png)
#### additional text
Add new text content after the existing text content.
![](564ad9f9e4d50.png)
#### Color
Set the text color. The default value is “black”.
![](564ad9f9d0e07.png)
#### Font
Set text font. The default value is “Song”.
![](564ad9fa147d3.png)
#### Font size
set font size of text. The default value is 12.
![](564ad9fa23aae.png)
#### Horizontal alignment type
set alignment type of text. The default value is “horizontal center” and the options are:
-  left alignment
-  right alignment
- horizontal center

![](564ad9f984c7f.png)
#### Vertical alignment type
set the vertical alignment type of text. The default value is “vertical center”, and the options are:
- upper alignment
- lower alignment
- vertical center

![](564ad9f9243f6.png)
#### Bold
set if text is bold or not. The default value is “bold”.
![](564ad9f940ede.png)
#### Italic
Set if the text is italic or not. The default value is “italic”.
![](564ad9f9b4638.png)
#### Upper limit of characters
Set the upper limit of characters number in text field. The default value is 100.
![](564ad9fa081d9.png)
#### Password display
Set if display as password form or not. the default value is “password”.
![](564ad9f97669e.png)
#### Dynamic/inputable
Set it’s dynamic text or inputable text. The default value is “dynamic”.
![](564ad9f95a82a.png)
#### Line break
Set the text support line break or not. the default value is “support”.
![](564ad9f969f63.png)


