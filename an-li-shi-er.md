# 案例十二：有限状态机

##案例介绍

有限状态机，（英语：Finite-state machine，FSM），又称有限状态自动机，简称状态机，是表示有限个状态以及在这些状态之间的转移和动作等行为的数学模型。它反映从系统开始到现在时刻的输入变化，转移指示状态变更，并且用必须满足来确使转移发生的条件来描述它；动作是在给定时刻要进行的活动的描述。

## 案例准备
我们举一个例子，我们平时在自动售货机上买饮料，自动售货机的内部实际上就是一个有限状态机：
假如有这样一个自动售货机，售卖苏打汽水，它有如下五种输入：
输入0 -- 存入25美分
输入1 -- 存入1美元
输入2 -- 取汽水
输入3 -- 退币
输入4 -- 退出系统

![](/assets/p2009.png)

![](/assets/p2010.png)

## 案例实现

![](/assets/p2011.png)

其实Freduino小车就是通过有限状态机来实现的，我们可以把小车的行为依依列举出来，比如左右转，前进，发出声波，光线，声音等，我们只要通过控制这些状态就能控制小车完成各样的工作：

![](/assets/p2012.png)


你能自己设计出一个更加复杂的售货机么？



