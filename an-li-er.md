# 案例二：读心数

## 案例介绍
本案例将指引学生利用Scratch Blocks编程界面现有的块和功能设计一个互动猜数字小游戏，通过键盘录入输入猜的数字，程序会给出提示，直到猜到正确的数字。

![](/assets/anli-two.jpg)

## 案例准备
其知识点涵盖编程语言的逻辑结构，循环结构，以及变量的设定。分析知识点关联，编写详细的教学案例指导手册，并提供相应的代码。

知识模块主要包括：
a：二分法的概念。
b：程序结构的设计（顺序结构，循环结构）。
C：学习键盘录入的使用方法。

a: 二分法（dichotomie） 即一分为二的方法。设[a，b]为R的紧区间， 逐次二分法就是造出如下的区间序列([an，bn])：a0=a，b0=b，且对任一自然数n，[an+1，bn+1]或者等于[an，cn]，或者等于[cn，bn]，其中cn表示[an，bn]的中点。
Java代码：
public int binarySearch(int[] data,int aim){//以int数组为例，aim为需要查找的数

int start = 0;

int end = data.length-1;

int mid = (start+end)/2;//a

while(data[mid]!=aim&&end>start){//如果data[mid]等于aim则死循环，所以排除

if(data[mid]>aim){

end = mid-1;

}else if(data[mid]

start = mid+1;

}

mid = (start+end)/2;//b，注意a，b

}

return (data[mid]!=aim)?-1:mid;//返回结果

}

b:本案例着重讲解程序结构的设计，本案例设计到两个角色，第一个角色有着回答窗口，计数器功能，所以需要有三个变量，一个变量用于键盘录入，另一个变量用于计数器计数，最后一个用于储存在1到100间随机生成的一个数，先将计数器的值归零，然后在1到100中随机生成一个数放入变量“数字”里面，当执行“询问…并等待”时，角色1会发出询问，并提供一个回答的窗口，这个窗口就是用于键盘录入的，会被存入变量“回答”中。这时，程序会进入循环结构，只有当键盘录入的数字与随机生成的数字相同时才会停止循环，循环结构里面包含了一层选择结构，分别是当猜的数字过大或过小时，角色1会做出的反应。当猜的数字与随机生成的数字相同时，使角色2显示，其它时候隐藏。代码图如下：

![](/assets/anlitwo-two.jpg)

C:当使用ask…and  wait 时，scratch界面会给出如图所示用于键盘录入的窗口：

![](/assets/anlitwo-three.jpg)