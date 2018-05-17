#案例十一：我的BLOCKLY我做主

##案例简介
  通过浏览Blockly的Code界面和文件目录，不难发现它其中带有大量的预定义块，从数学函数到循环结构都包含在内，然而为了与外部应用程序交互，必须创建自定义块以形成API。例如，当创建绘图程序时，可能需要创建“半径R的绘制圆”块。而在大多数情况下，最简单的方法是找到一个已经存在的相似的块，复制它，并根据需要修改它即可。
  
  ![](/assets/anlieleven-one.png)
  
  在Blockly Demos文件中，有一个Blockly开发者工具（Blockly Developer Tools），我们可以借助这个工具进行块的快速设计与实现，定制个人专属的Blockly，这使得Blockly可扩展性大大提升，同时也是Blockly的灵活和强大之处。这使得Blockly可扩展性大大提升，同时也是Blockly的灵活和强大之处。本案例面向具有一定的HTML和JavaScript编程基础，并希望在Blockly中创建自定义块的教师或学生。
  
## 案例准备
在案例正式开始之前，先给大家介绍一些基础的知识，方便师生对案例的理解与消化。

## 1.自定义块的简单步骤

块的自定义工作主要分为三个步骤，分别是：

第一步是创建一个块，指定其形状，字段和连接点。使用Blockly Developer Tools是编写此代码的最简单的方法，或者，可以在学习API之后手动编写该代码，高级块可以响应用户或其他因素而动态地改变它们的形状。

第二步是创建生成器代码，将新块导出为编程语言（例如JavaScript，Python，PHP，Lua或Dart）。为了生成既干净又正确的代码，必须注意给定语言的操作列表顺序，创建更复杂的块需要使用临时变量或调用函数，当Input功能使用两次并需要缓存时，这是尤为重要的。

第三步是导入Code界面，当完成块的外观和代码定义之后，即可通过修改Code的HTML文件，将设计的块添加到Toolbox中，进而呈现在Code的Web界面。

## 2.Block Factory简介

![](/assets/anlieleven-two.png)

定义一个块需要使用到Blockly开发工具中的块工厂(Block Factory),块工厂主要分为三个区域：

(1)编辑区：对新增块进行设计和编辑
(2)预览区：对编辑区编辑的块进行实时预览
(3)代码区：代码区分为两个部分Language code和Generator stub，其中Language code 区指定和控制新增块所呈现的形状，Generator stub区负责新增块所要生成的代码。

在编辑区的左侧，可以看到4个基本块，Input，Field，Type和Colour，它们是四个原料库，使用者可以从这些库中获取所需要的任意“原料”，来合成自己的新块。

![](/assets/anlieleven-three.png)

### （1）Colour

先从最简单的介绍，颜色(Colour)块，它默认定义了九种基本颜色，直接将你想要的颜色拖到右侧，拼接到对应的colour的凹槽，便可立即在预览区看到新块的颜色。

![](/assets/anlieleven-four.jpg)

![](/assets/anlieleven-five.png)

如果默认色彩中没有你想要的颜色，可以拖动任意色彩块到编辑区拼接完成后，点击色块中的数字，在色块的下方出现一个圆形的调色盘，转动调色盘，选择你喜欢的颜色。

![](/assets/anlieleven-six.png)

在Blockly中，同一类型的块通常采用相同的颜色，所以新块的颜色选择不能仅凭喜欢，还需要前后兼顾。

一个新块不仅需要有颜色，还需要与其他块进行衔接，这就需要设计新增块的输入和输出，它们将决定新增块的功能、属性和类别。

接下来看一看输入(Input)，这是新增块与其他块连接的接口之一。

### （2）Input

![](/assets/anlieleven-seven.png)

输入可以分为三种类型：值输入(value input)，声明输入(statement input)，模拟输入(dummy input)。首先以值输入为例，拖动值输入至右侧与Inputs连接，可看到预览区新增块多了一个凹槽:

![](/assets/anlieleven-eight.png)

根据需要，使用者还可以添加多个输入值，但要注意多个输入值的名字不能相同，否则会出现警告，而且在后续调用的时候，也会冲突报错，新块名字也是如此，不能与其他块同名，就好比如果班里有两个学生名字一样，那老师点名提问的时候就有可能出现两个同学同时起立的尴尬。

![](/assets/anlieleven-night.png)

在值输入中还可以添加域(field)，比如加入最简单的文本域，即可在输入中提示对应的文本，域中的下拉选择框可设置文本的对齐方式。

![](/assets/anlieleven-ten.png)

这些设置完毕，选择新块的输入方式，扩展式和嵌入式：

![](/assets/anlieleven-tw.png)

![](/assets/anlieleven-eleven.png)

有了输入之后，别的块就可以很容易的通过凹槽加入到新块了，但是，这时另外一个值得考虑的问题又出现了，怎样将新增块加入到其他的块之中呢？我们有五种选择：

![](/assets/anlieleven-t.png)

看完值输入之后，再一起来看一下另一个常用的输入类型，声明输入(statement input)，它通常用作条件控制和循环控制。

![](/assets/anlieleven-f.png)

使用值输入和声明输入，可以很容易的设计出编程中常用的条件语句和循环语句：

![](/assets/anlieleven-fi.png)

看了这些Block Factory常用知识之后，我们一起来看一下本案例的具体内容。



# 案例内容
本案例将和您一起见证一个“Hello World”模块从诞生到使用的过程。
首先，您可参照案例知识准备环节的内容，对您的块的外观进行设计，完成设计之后，剩下的过程可以分为3步：

##第一步

![](/assets/anlieleven-s.png)

在您创建块的Blockly Developer Tools界面，将上图区域中的代码选中复制，然后在blockly文件夹中，找到名为blocks的文件夹，进入：

![](/assets/anlieleven-se.png)

在blocks文件夹中，新建一个test.js文件。

![](/assets/anlieleven-ei.png)

将复制的代码粘贴到js文件中，并添加如下图所示3行代码(蓝色选中区域)，保存。

![](/assets/nine.png)

##第二步

![](/assets/ten.png)

将上图区域中的代码选中复制，然后在blockly文件夹中，找到名为generators的文件夹，进入

![](/assets/eleven.png)

再进入名为javascript的文件夹中，新建名为test.js文件

![](/assets/tw.png)

将复制的代码粘贴到js文件中，并添加如下图所示3行代码(蓝色选中区域)，保存。

![](/assets/tt.png)

## 第三步

对html文件进行修改，将自定义块呈现给用户。
### 1.在html文件中添加对前两步所创建的2个test.js文件的引用。

![](/assets/tf.png)

【注】
这两行代码添加的位置需要注意，一定要添加在<script src=”…/…/javascript_compressed.js”></script>这行之后，不然引用时候的先后顺序会使其失效，这里保险起见，我直接添加在了相对靠后的位置。

### 2.在工具箱(toolbox)中添加创建的自定义块

![](/assets/ts.png)

在html文件中，标签<xml id=”toolbox” style=….>………</xml>之间所控制的就是工具箱中所显示的内容，其中<category>标签控制的是工具箱中的类，<block>标签控制的是类中的块。由于类和块属于包含关系，所以对于同一个工具箱而言，只要有一个块有其对应的类，其余所有的块都需要创建其对应的类，否则会导致所有的块和类都无法显示（这里您可能不太好理解，举个例子，把“类”比作汽车，“块”比作人，参加一个马拉松比赛，要么大家都不开车，不然，只要有一个人开车，为了比赛的公平性，其他所有人也必须开车。如果一部分人开车，一部分人不开车，那工具箱就无法对比赛结果进行衡量了，就出现页面崩溃的现象）。
所以在对此html文件进行修改添加新建的自定义块时，我们取类的名字为“测试”，在“测试”类中添加test块。

![](/assets/tse.png)

保存，然后刷新浏览器即可看到新建的自定义块。
至此，关于Blockly二次开发教学案例“我的Blockly我做主”就完成了。






 



