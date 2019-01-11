![](5653f6ad2b542.png)

The English name of Bitmap Font is Bitmap Font, which is very common in game production.In order to match the overall style of the game, some special fonts or artistic fonts are often needed.The combat effectiveness value in the figure below is realized by bitmap font:
![](5653f6ac4fb50.png)![](5653f6ac72114.png)
If the font library of special font or art font is built into the game directly, it will slow down the loading and running speed of the game.Bitmap fonts are a good solution to this problem.The method of bitmap font is to make a bitmap of the corresponding font of each word to be used, generate the mapping between the text content and the bitmap, and display the bitmap dynamically in the game. In this way, beautiful fonts are presented in the game and resources are saved.

The bitmap font used in Laskshore consists of a PNG image set and an FNT configuration file.The PNG image set contains all the bitmaps that will be used, and the FNT configuration file describes how these bitmaps should be split from the PNG image set.

It is recommended to use Egret TextureMerger to draw the type of bitmap font used by Lakeshore. Please refer to the Bitmap font section of the TextureMerger tutorial：[TextureMerger](http://bbs.egret.com/thread-1653-1-1.html)

------------


### Specific Attribute
![](5653f6ace22a2.png)
- Texture image: PNG image specifying bitmap font.
- Configuration file: FNT configuration file that specifies a bitmap font.
- Default text: the text content displayed by default.
- Character spacing: the character spacing of a bitmap font. The default value is 0.
- Line spacing: the line spacing of a bitmap font. The default value is 0.

------------


### Bitmap Font Conditions
![](5653f6ad006eb.png)
#### Comparison of the content
Compares the text content of a bitmap font to the specified content, if the same is true.【持续性触发】【 continuous trigger 】
![](5653f6ad1baba.png)

------------


### Bitmap Font Action
![](5653f6ac8be71.png)
#### The text content
Sets the contents of the bitmap font display.
![](5653f6acac34b.png)

#### Append text
Appends text to existing content in bitmap fonts.
![](5653f6acbb211.png)

#### Between characters
Sets the character spacing of bitmap fonts.
![](5653f6acc5ea9.png)

#### Line spacing
Sets the line spacing of bitmap fonts.
![](5653f6ac94db2.png)

