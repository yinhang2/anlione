# 案例八：函数图像生成器

##案例介绍
本案例通过修改Blockly底层代码制作一个Blockly函数图像生成器，如下图所示，左侧为代码编辑区域，而右边则会生成相对应的函数图像。
 
 ![](/assets/anlieight-one.png)
 
 ![](/assets/anlieight-two.png)
 
##案例准备

本案例需要对JavaScript和HTML语言有一定的基础，并对Blockly底层代码有一定的了解，能够清晰的了解Blockly各文件的功能。

## 案例开发
首先在blockly/demos/code/index.html文件中找到可以放置函数图像模块的位置，可以在&ltbody&gt标签中找到blockly的布局是通过&lttable&gt标签进行放置的：

![](/assets/anlieight-two.jpg)

所以我们在table标签中找到一块地方放置函数图像：

![](/assets/anlieight-three.jpg)

函数图像的显示是通过XCalc来实现的，其代码是用javascript编写，所以我们直接将js代码嵌入html进行初始化显示，初始化显示(x+4)^2*(x-6)+60sinx函数

![](/assets/anlieight-four.jpg)

新建blockly模块，用于拖拽进行不同函数显示，新建模块使用blocklyfactory进行设计实现：

![](/assets/anlieight-five.jpg)

将设计好的模块插入到index.html进行显示：

![](/assets/anlieight-six.jpg)

模块将输入的函数（如上图所示的sinx）转换成$sinx这样的javascript代码，当用户点击运行按钮后，程序执行code.js文件中的code.runJS()函数

![](/assets/anlieight-se.jpg)

通过Blockly.JavaScript.workspaceToCode(Code.workspace)函数会获取到用户生成的函数代码，通过XCalc将函数图像显示出来。





