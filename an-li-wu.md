# 原码反码和补码

## 案例介绍
数在计算机中是以二进制形式表示的。
数分为有符号数和无符号数。
原码、反码、补码都是有符号定点数的表示方法。
一个有符号定点数的最高位为符号位，0是正，1是副。
本案例将为大家介绍如何用Blockly实现输入一个十进制数，输出这个数的原码反码和补码。

## 案例准备
**原码**：是指符号位用0或1表示，0表示正，1表示负，数值部分就是该整数的绝对值的二进制表示。例如：假设机器数的位数是8，那么：[+17]原=00010001 [-39]原=10100111

**反码**:在反码的表示中，正数的表示方法与原码相同；负数的反码是把其原码除符号位以外的各位取反（即0变1，1变0）。通常，用[X]反表示X的反码。例如： [+45]反 = [+45]原 = 00101101，[-32]原 = 10100000，[-32]反 = 11011111

 **补码**:在补码的表示中，正数的表示方法与原码相同；负数的补码在其反码的最低有效位上加1。通常用[X]补表示X的补码。例如： [+14]补 = 10100100,[-36]反 = 11011011,[-36]补 = 11011100

实事求是地说，引入补码意义非同寻常，可以说是先辈们智慧的结晶。因为，通过补码运算，可以把减法运算变成加法运算；而乘法可以用加法来做，除法可以转变成减法。这样一来，加、减、乘、除四种运算“九九归一”了。这对简化CPU的设计非常有意义，CPU里面只要有一个加法器就可以做算术运算了。

![](/assets/1013.png)

因此只要能将数字转化为二进制机器数，那么就可以模拟计算机完成各种数值运算，实现加减乘除的功能。下面我们来一起将正负数的十进制数转化为二进制：

## 案例实现
1、正数的原码反码和补码都是相同的，因此只要求出一个即可，我们通常用栈来实现向二进制的转换，blockly提供list作为指针数组可以实现栈的操作，如下图所示：

![](/assets/p2000.png)

栈操作实际上就是一种先进后出的数据结构：

![](/assets/p2002.png)

我们举一个例子，比如求29的原码，那么过程如下：

![](/assets/p2003.png)

![](/assets/p2004.png)

list数组提供从头尾插入和删除元素，并能在指定位置提取元素：

![](/assets/p2001.png)

因此我们只要依次将求出的余数从数组头处插入即可，读取数组的时候从头到尾开始阅读。

![](/assets/p2005.png)

2.负数的原码其实内容上和正数是一样的，只是符号位与正数是不同的，我们之所以把数设置成8位，就是为了留出1位作为符号位，因此8位数可以表示-128~127，第一位表示符号位，0为正数，1为负数，所以-29二进制表示为：10011101。
 负数的反码就是符号位不变，其余位取反，反码的意义就在于进行下一步取补码。负数的补码就是反码加1，求出补码的算法就是从最后一位开始判断，如果是0，就将其变为1，如果是1，就判断倒数第二位，依次类推，你可以举几个例子自行判断一下。

![](/assets/p2007.png)

![](/assets/p2008.png)











