# 案例九：走进古诗词

## 案例介绍
本案例通过修改Blockly底层文件做出“走进古诗词”这一案例，在“走进古诗词”这一案例中，Blockly的界面中会产生不同的诗句以及诗人，而我们要做的就是将诗人与诗句匹配起来。

![](/assets/anlinine.png)

## 案例实现
### 1.准备拼图块：
首先，我们以诗词为例，从唐诗三百首中挑出8首，通过javascript代码来添加block的“长相”：创建shici_pintu_look.js文件，为了让用户可以拼图，我们将四行诗句其中某一行取出，并将作者杜甫去掉，使这两个内容以单独的块出现。将其他三行诗句与诗名放在一个代码块中，例如下图所示《天末怀李白》，可见该块有两个输入(Input)：一个ValueInput和一个StatementInput。分别用于接收一个作者和一句诗的代码块嵌入。

![](/assets/anlinine-one.png)

这首诗充当一个Master（后文将解释何为Master与Sub）块。下面的两个块分别是该Master块的唯一正确答案，以Sub块的形式出现，与上面的Master块直接对应。

![](/assets/anlinine-two.png)

上述代码所创建的3个块“长相”如下图所示：

![](/assets/anlinine-three.png)

Sub块必须对应且仅与唯一一个Master块相对应，我们将8首诗每一首都分解为上面的三个代码块：一个Master带有3行诗句，一个Sub包含剩余的一句诗，另一个Sub包含这首诗的作者。分别命名为：shici_n,points_on_shici_n，points_on_shici_n_1：n从1到8。共3*8=24个代码块。

### 2.设计界面：
为了简便，我们就不从头开始设计界面了，而是直接修改Blockly源代码附带的code应用界面，该应用的文件目录是Blockly\demos\code\index.html。这个Code应用主要由index.html来描述界面，由code.js负责主要的javascript代码，包括Blockly editor在html中的插入、不同语言的tab切换以及javascript代码运行等逻辑的实现。
我们仅保留下面的Blockly editor所需div，并留下一个按钮，将它修改为“检查答案”，就可以得到一个清爽的界面。

![](/assets/anlinine-four.png)

由于拼图不需要左边的toolbox，并且每个块只出现一次。因此要去掉toolbox：在Blockly.inject当中将toolbox参数设置为null。

![](/assets/anlinine-five.png)

![](/assets/anlinine-six.png)

没有toolbox之后，用户将无法从toolbox中拖拽添加块到workspace当中，为了让用户“有块可拼”我们调用Code.loadBlocks（位于原code.js中）自动添加块，该函数接收一个参数：描述块位置的xml代码。我们给它传递了一个变量：shiciPintuBlocks，定义如下： 

![](/assets/anlinine-se.png)

可以看到，我们最初一共设计了8套诗词的块，这里我们添加了其中的4套，共4*3=12个块。完成上述代码后，运行index.html将得到如下图所示界面，右上角的“检查答案”按钮用于检查用户当前的拼图是否正确。 

![](/assets/anlinine-eight.png)

### 块的代码构成
目前我们的拼图案例仅有表皮，没有内脏，为了实现拼图最重要的功能：答案检查功能，我们将给这些块添加代码，并编写检查答案的程序。首先我们将块分为Master和sub两种。Master是主要拼图块，Sub附属于Master。Sub分为两类： 一类是下拉菜单，另一类是拼接上去的块：这种块又分为Value Input和Statement Input，它们本质上的区别不大，具体选择使用哪一种主要基于拼图过程中块该以哪种形状出现能更方便表达意义而定。如上面诗词的例子，作者更适合出现在题目的右侧，因此选用Value Input类型，而其中的一句诗词应当与上面的诗词并列，因此选用Statement Input类型。
由于我们的Sub块必须连接一个Master块，并且一个Sub仅对应唯一一个Master块，因此我们为Master设计一个编号（每个Master块编号必须不同），与该Master对应的块所生成的代码必须包含该Master编号。我们建立shici_pintu_code.js文件，用于保存上面创建的24个块的生成代码。一个Sub块的代码生成函数如下：

![](/assets/anlinine-nine.png)

这两个函数分别对应Master块《天末怀李白》这首诗中的作者“杜甫”和其中的一句诗句“文章憎命达，魑魅喜人过”。可以看到这两块的代码仅仅十分简单的返回了一句’S(#101);\n’。这里的格式为S(#编号)，S代表这是一个Sub块，#编号指定该Sub块所对应的唯一Master块的编号，下面是《天末怀李白》这首诗的Master代码块生成代码：

![](/assets/anlinine-ten.png)

可以看到它所返回的code变量由M(#101){statements_name+value_name}构成。#101正好是该Master的编号，与上述Sub一致。Statements_name来自诗句的输入，value_name来自作者的输入。如果这两个位置正好拼对，都会返回“S(#101);\n”这个字符串。其次，请注意红框所框出的代码，它的作用是：当用户没有拼接Master块的空缺，valueToCode或statementToCode函数将返回NULL，此时value_name或statements_name就等于*。这个星号的作用是标明一个错误（之后在验证答案代码中可以见到这种情况）。
   另外，如前所述，Master除了接收拼图外，还可以内含一个单选下拉框，在设计下拉框几个选项的返回值时，我们规定，以’^’符号为正确，以’*’符号为错误。
   综上所述：Master块返回代码形式为：M(#X){Sub1,Sub2.....}，X为该Master编号，以大括号{}包括所有的Sub Input所返回的代码；下拉菜单选项：*是错误符号， ^是正确符号；Sub块代码：S(#X) 这里的编号须和M(#X)的编号X对应。

### 验证函数：
用户点击右上角的“检查答案”按钮后，将调用CheckAnswer函数，该函数总体结构下：（代码太长，对while函数做了缩进）

![](/assets/anlinine-ele.png)

其中Answersheet变量用来接收通过workspaceToCode函数所生成的完整代码（目前用户拼图所产生的代码）。Pos变量用来跟踪当前对Answersheet的parse位置。IsAllPassed布尔值用来标记拼图答案是否正确。首先对整个Answersheet搜索’*’符号（记得前一节我们定义’*’为错误符号）。若其中存在*符号，必然有Master块缺少Sub嵌入或存在选项错误的情况，直接判定失败。隐藏的while代码块用于对整个Answersheet以Master块为单位进行Parse. 展开while代码块如下所示（其中if内部嵌套了第二个while,我们也进行了隐藏）

![](/assets/anlinine-tw.png)

在上图所示while代码块中，首先我们对M标志进行搜索，若搜索到M，则表明一个新的Master块开始，同时以PrevPos记录之前的pos变量值（该值保存着前一个Master块的末尾位置）。接下来使用PrevPos为起始位置对’S’(Sub块）进行搜索。这样做的目的是为了寻找可能存在于两个Master代码之间的Sub块代码（这意味着该Sub块没有被拼接到任何Master块上）。以floatingSpos < pos来确认上述错误，并以pos == -1和floatingSpos != -1来判断是否存在游离于所有Master块代码最后的Sub块。 做完这些检查后，将检索’#’标志和’)’标志，这样做的目的是为了提取出Master块的编号，同时找到’}’符号，确认Master块的结尾位置。这三者都存在的情况下（if判断三个变量值不为-1），启用下一个while循环，遍历该Master块代码中包含的所有Sub块，隐藏的while部分如下所示：

![](/assets/anlinine-threeteen.png)

在每一次while循环当中，将对’S’进行搜索，若搜索到，通过寻找’(#’和’)’提取该Sub块的编号，然后将该编号与外层while循环提取出的Master块编号进行比较，若不一致，则声明验证失败,break退出。
以上就是整个CheckingAnswer函数的代码逻辑。在这一整套关于Master块和Sub块的定义、代码格式和错误符号的基础上，用户应该能够创建自己的拼图块，使用同样的CheckingAnswer函数对这些符合标准的块进行验证。
下图为CheckingAnswer所检查出错误后的提示：

![](/assets/anlininefourteen.png)

将上面的拼图完成后，点击“检查答案”获得成功提示：

![](/assets/anlinine-fifteen.png)

为了进一步提高生成拼图代码块的效率，若开发者有余力，可以自行开发拼图块的自动生成器，将古诗词从文本格式自动转化为block，提高开发效率！

“走进诗词”案例通过上述24个代码块的方法已经能够扩充题库，形成一个更加完整的拼图教育案例。接下来，我们也能够通过上述基础架构来创建一些有关地理的拼图模块，构成下一个案例“我们的地球”。 














    

