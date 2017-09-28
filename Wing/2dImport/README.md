
## 项目创建
- 点击导航栏“`文件`”->“`新建项目`”，弹出“`新建项目`”下拉菜单。**<font color=red> 如下图：</font>**
	
	![image](20170904171649.png)

- 选择项目类型，如：空Egret项目、Egret游戏项目、Egret EUI项目等，此处以Egret EUI项目为例。在上图下拉菜单中选择“Egret EUI项目”，弹出“`创建EUI项目`”面板，**<font color=red> 如下图：</font>**

	![image](20170904172957.png)
	![image](20170904173224.png)
	
   - 1区域：设置舞台的项目名称和项目路径。

   - 2区域：项目依赖的扩展库。

   - 3区域：设置舞台属性和引擎版本号。

   - 4区域：设置屏幕适配方式，包括缩放模式和旋转模式。

- 点击`完成`按钮。

	**<font color=red>如下图</font>：**
	
	![image](20170904174006.png)

   - 1区域：菜单栏和工具栏

   - 2区域：文件目录

   - 3区域：项目输出日志信息
   
   - 4区域：代码编辑区域
	

## 项目运行

在菜单栏的`项目`选项卡下：
	
- ### 构建
	- 编译当前项目  

- ### 清理
	- 清理项目，清理bin-debug中所有文件，然后生成js

- ### 调试\F5
  **<font color=red> 如下图：</font>**
  
  ![image](20170904174612.png)
   - 点击项目->调试 
   - 1区域：变量
   - 2区域：观察表达式
   - 3区域：调用栈
   - 4区域：断点设置
   - 5区域：调试操作，`继续`、`单步跳过`、`单步跳入`、`单步跳出`、`重启`、`结束`

[点击查看调试详情](../debug/inspector/README.md) 		



## 目录结构介绍
- wing项目目录	
		- .wing
			- launch.json
			- setting.json
			- tasks.json
		- bin-debug
		- libs
			- modules
				- egret
				- eui
				- res
				- tween
				exml.e.d.ts
		- promise
		- resource
			- assets
			- config
			- eui_skins
			- default.res.json
			- default.thm.json
		- src
		- templete
		- egretProperties.json
		- favicon.ico
		- index.html
		- tsconfig.json
		- wingProperties.json
		
各目录的作用可以查看[文档](../../Engine2D/getStarted/helloWorld)

## EUI 相关信息

### 新建 EXML
+ 右键点击eui_skins

	**<font color=red>如下图：</font>**

	![image](20170904181052.png)
+ 点击`设计`页签。

  **<font color=red>如下图：</font>**

	![image](20170905093913.png)
	
	
	- 1区域：eui的编辑模式，`设计`，`动画`，`预览`，`源码` 三种模式。
	
	- 2区域：设计区域、动画编辑、预览、源码编辑。
	
	- 3区域：EXML的编辑面板		
	    - 资源库：在default.res.json中配置的资源。
		
		- 状态：自定义状态，例如：TestButtonSkin.exml 中有三个状态up、down、disabled，可以单独设置TestButtonSkin单独某个状态的皮肤。
		
		- 组件：系统控件(Button、CheckBox、CheckBox等组件)、布局组件(Group、Panel、Scroller、ViewStack)、自定义组件。
		
		- 图层：TestButtonSkin包含图层。
		
		- 属性：包含常用、样式、大小和位置、布局。
		
  **<font color=red>如下图：</font>**

	![image](20170905095155.png)
		
		

- 详细内容 [EXML可视化编辑](../editor/exml/README.md) 

### 资源管理 [点击详情](../editor/resdepot/README.md) 

