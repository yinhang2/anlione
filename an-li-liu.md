# 牛顿迭代法

## 案例介绍
牛顿迭代法（Newton's method）又称为牛顿-拉夫逊（拉弗森）方法（Newton-Raphson method），它是牛顿在17世纪提出的一种在实数域和复数域上近似求解方程的方法。牛顿迭代法是求方程根的重要方法之一，其最大优点是在方程f(x) = 0的单根附近具有平方收敛，而且该法还可以用来求方程的重根、复根，此时线性收敛，但是可通过一些方法变成超线性收敛。另外该方法广泛用于计算机编程中。

![](/assets/0.jpg)

## 案例准备
设r是的根，选取作为r的初始近似值，过点做曲线的切线L，L的方程为，求出L与x轴交点的横坐标，称x为r的一次近似值。过点做曲线的切线，并求该切线与x轴交点的横坐标，称为r的二次近似值。重复以上过程，得r的近似值序列，其中，称为r的次近似值，上式称为牛顿迭代公式。

用牛顿迭代法解非线性方程，是把非线性方程线性化的一种近似方法。把在点的某邻域内展开成泰勒级数，取其线性部分（即泰勒展开的前两项），并令其等于0，即，以此作为非线性方程的近似方程，若，则其解为，这样，得到牛顿迭代法的一个迭代关系式。

已经证明，如果是连续的，并且待求的零点是孤立的，那么在零点周围存在一个区域，只要初始值位于这个邻近区域内，那么牛顿法必定收敛。并且，如果不为0,那么牛顿法将具有平方收敛的性能.粗略的说，这意味着每迭代一次，牛顿法结果的有效数字将增加一倍。

军人在进攻时常采用交替掩护进攻的方式，若在数轴上的点表示A，B两人的位置，规定在前面的数大于后面的数，则是A>B，B>A交替出现。但现在假设军中有一个胆小鬼，同时大家又都很照顾他，每次冲锋都是让他跟在后面，每当前面的人占据一个新的位置，就把位置交给他，然后其他人再往前占领新的位置。也就是A始终在B的前面，A向前迈进，B跟上，A把自己的位置交给B（即执行B=A），然后A再前进占领新的位置，B再跟上，直到占领所有的阵地，前进结束。像这种两个数一前一后逐步向某个位置逼近的方法称为迭代法。

迭代法也称辗转法，是一种不断用变量的旧值递推新值的过程，跟迭代法相对应的是直接法（或者称为一次解法），即一次性解决问题。迭代算法是用计算机解决问题的一种基本方法。它利用计算机运算速度快、适合做重复性操作的特点，让计算机对一组指令（或一定步骤）重复执行，在每次执行这组指令（或这些步骤）时，都从变量的原值推出它的一个新值。

利用迭代算法解决问题，需要做好以下三个方面的工作：

一、确定迭代变量

在可以用迭代算法解决的问题中，至少存在一个可直接或间接地不断由旧值递推出新值的变量，这个变量就是迭代变量。

二、建立迭代关系式

所谓迭代关系式，指如何从变量的前一个值推出其下一个值的公式（或关系）。迭代关系式的建立是解决迭代问题的关键，通常可以使用递推或倒推的方法来完成。

三、对迭代过程进行控制


在什么时候结束迭代过程？这是编写迭代程序必须考虑的问题。不能让迭代过程无休止地执行下去。迭代过程的控制通常可分为两种情况：一种是所需的迭代次数是个确定的值，可以计算出来；另一种是所需的迭代次数无法确定。对于前一种情况，可以构建一个固定次数的循环来实现对迭代过程的控制；对于后一种情况，需要进一步分析得出可用来结束迭代过程的条件。

##案例实现
Java开平方根代码——————牛顿迭代法<br&gt; 
package project.test;<br&gt;
import java.math.*;<br&gt;  
public class SqrtTest {<br&gt;  
private static final String num = "10";<br&gt  
private static final int accuracy = 5; <br&gt 
private static double accuracyDouble = 0.1;<br&gt
public static void main(String[] args) {<br&gt
calSqrt();<br&gt
}<br&gt

private static void calSqrt() {<br&gt
BigDecimal guessNum = new BigDecimal(1);<br&gt
for (int i = 0; i < accuracy; i++) {
accuracyDouble *= 0.1;
}
while (true) {
BigDecimal temp = SqrtTest.newtonMethod(guessNum);
if (temp.equals(guessNum)) {
break;
}
double d = guessNum.subtract(temp).doubleValue();
if (d > 0 && d < accuracyDouble) {
guessNum = temp;
break;
}
guessNum = temp;
}
System.out.println("Result is " + guessNum);
}


private static BigDecimal newtonMethod(BigDecimal guessNum) {
return guessNum.subtract((guessNum.multiply(guessNum).subtract(new BigDecimal(num))).divide(new BigDecimal(2).multiply(guessNum), accuracy, BigDecimal.ROUND_HALF_EVEN));
}


}

Blockly实现：

![](/assets/anliniu.png)