# 案例十：我们的地球

##  案例介绍
本案例为将为大家详细讲解如何利用现有Blockly底层文件制作出“我们的地球”这一案例，在这一案例中，将会有“亚洲”、“欧洲”、“非洲”、“北美洲”、“南美洲”、“大洋洲”等几个大洲，而我们要做的就是将一些国家名按照这六个大洲分类。如下图所示：

![](/assets/anliten-one.png)

将上面的拼图完成后，得到成功提示：

![](/assets/anliten-twp.png)

## 案例实现
###动态生成块的定义：
本案例使用“走进诗词”案例中已经编写好的拼图代码框架，并加入一些新的随机生成功能。我们以大洲和国家对应来设计拼图块，先从网上搜集一些著名国家的信息，其中亚洲共48个国家，欧洲45个国家，非洲53个国家，北美洲25个国家，南美洲12个国家，大洋洲16个国家，南极洲没有国家。以“亚洲”、“欧洲”、“非洲”、“北美洲”、“南美洲”、“大洋洲”作为Master块，每一个洲的主要国家作为Sub块，将所有这些国家的信息放在JavaScript的Array数据结构中，定义如下：

![](/assets/anliten-three.png)

传统方法对每一个Blockly块的定义需要两个代码函数：Blockly.Blocks[]={};和Blockly.Javascript[] = function。之前我们的块都是在网页打开之前提前放好在JS文件当中的，由于在拼图应用当中涉及到的块数量非常多，而且当我们的题库达到一定程度后，就会需要非常多的块代码来支撑，这给编写块代码带来了很高的难度。为了简化块的代码编写，并且节省运行时内存中块的数量，我们引入了一种运行时动态自动生成块的技术，定义一个函数：

![](/assets/anliten-four.png)

该函数，有3个参数，分别是块名，所属的Master块（大洲）的ID，以及这个块显示的名字（国家名）。 为了让“我们的地球”拼图游戏呈现出随机性，我们让网页每次运行的时候，从上面定义的各大洲国家Array数据结构中随机抽取出几个国家生成相应的拼图块。
这里的动态生成代码如下：
生成大洲Master块的函数：

![](/assets/anliten-five.png)

生成国家Sub块的函数：

![](/assets/anliten-six.png)

通过调用上面两个函数，我们的javascript代码能够轻松的生成一个大洲的拼图块或一个国家的拼图块，为了生成6个大洲，每个大洲随机生成6个国家的块，我们编写如下生成代码：

![](/assets/anliten-seven.png)

其中，外层循环用于遍历大洲的Array，内层循环用于遍历某一个大洲内的国家，通过使用Math.random()函数随机从Array中选择国家来生成相应的拼图块，为了避免出现重复的国家，我们加入了AlreadyIn数组来记录之前已经生成的国家，在生成下一个国家之前，先检查该国家与AlreadyIn数组中已经有的国家是否有重复。

### 动态生成块集合的XML
由于块的数量太多，为了减少工作量，我们定义diliPintuBlocks的xml字符串，通过代码来自动生成xml代码，加入x和y变量，通过javascript的Math.random()函数随机生成块的其实坐标，从而实现每次刷新界面块的位置都不同的效果。

![](/assets/anliten-eight.png)










