# 案例一：会说话的程序猫

## 案例介绍
Blockly和Scratch Blocks作为功能强大、扩展性强的可视化编程工具，拥有着为今后信息技术教育和跨学科教学做出贡献的非凡潜力。Blockly核心功能虽然强大，却不支持多媒体和图形化的交互界面；Scratch Blocks是Blockly和Scratch的结合产物，作为可视化编程工具的新成员。

![](/assets/anlione.png)

本案例将指引学生熟悉Scratch Blocks的编程界面，并编写第一个Scratch Blocks小程序。此外，对于具有一定编程基础的师生，如果有兴趣对Scratch Blocks进行进一步的探究，可以进行本案例第二部分的学习，通过让学生亲自动手进行离线环境的搭建，了解Scratch Blocks的内部文件结构及其工作原理。

![](/assets/anlione-two.png)

## 案例准备
### 1.舞台（Backdrop）与角色（Sprite）更换
![](/assets/anlione-three.png)
以舞台为例，可以将Scratch的舞台更换成任意背景，目标舞台的来源分为4种情况：
（1）从素材库中进行选择（Choose a Backdrop）

![](/assets/anlione-four.png)

（2）手绘（Paint）

![](/assets/anlione-five.png)

（3）电脑中上传（Upload）

（4）随机选择（Surprise）

### 2.循环语句与顺序执行
案例中程序猫和唐老鸭的对话，需要用到Forever循环语句，需要提前对循环语句有所了解，并通过wait模块的使用，控制对话的顺序。

![](/assets/anlione-six.jpg)

循环知识的讲解：一群环卫工作人员需要为街道种上环保树。因此，针对每一棵树，园丁们需要：挖个坑、放入树苗、埋上土、前进5米，然后种下另一个棵树。如果街道长度是20米，种每棵树的步骤将重复4次。

![](/assets/anlione-seven.png)

在编程中，使用计数次循环积木指定循环的次数。有时，循环是永久的、无限的。比如说日出日落。在编程中，也会使用无限循环积木，使程序永久重复。循环与重复是同样的概念。如果你重复做一件事情，你就是在做一个循环。
循环的概念：机器反复不断地执行某段程序，可永久重复，也可重复指定的次数。


## 案例内容

## （一）会说话的程序猫

会说话的程序猫案例将实现程序猫与唐老鸭对话场景，涉及角色更换，舞台更换，顺序结构，循环结构，场景切换等知识点。
###  1.角色的导入
准备好Scratch程序猫和唐老鸭角色素材，并将素材通过“上传角色（Upload Sprite）”上传至舞台。

![](/assets/anlione-eight.png)

### 2.场景的替换
将对话场景进行替换，可从素材库中进行选择（Choose a backdrop），也可以从本地上传（Upload a backdrop）。

![](/assets/anlione-nine.png)

### 3.对话内容的设计
确定Scratch小猫和唐老鸭的对话内容，分别选定角色，编写各自的控制程序，然后通过wait指令，调整对话框弹出的先后顺序。

### 4.程序调试
待程序编写完成之后，点击开始按钮，对对话内容进行跟踪调试，并对程序进行优化。

## (二)我的SCRATCH BLOCKS
如果你想对Scratch Blocks有进一步的了解，或者想在自己的电脑或服务器上搭建Scratch Blocks的环境，供教学和研究使用，您可以参照下面的内容。
本案例结合Github上开源项目，进行Scratch Blocks相关环境的配置。整个环境由3部分组成，分别是scratch-vm, scratch-blocks和scratch-gui。
注：中间个别指令可能需要管理员(root)权限，为避免切换，整个过程最好是在管理员(root)用户下进行操作。

1.准备工作
/* git, npm, nodejs工具准备 */

/* Linux下安装指令 */
sudo apt-get install npm
sudo apt-get install nodejs
sudo apt-get install git

/* 对版本要求较高，需升级 */
npm install -g npm      /* npm升级到最新版本 */
npm install -g n        /* nodejs升级 */
n stable                /* 升级到最新的稳定版本 */

mkdir scratch  /*便于管理，新建一个文件夹存放*/
cd scratch
git clone https://github.com/llk/scratch-gui     /*scratch-gui下载*/
git clone https://github.com/llk/scratch-vm      /*scratch-vm下载*/
git clone https://github.com/llk/scratch-blocks  /*scratch-blocks下载*/

2.Scratch-VM的配置
cd scratch-vm
npm install
npm link
npm run watch
注：在执行”npm run watch”时，会停留在”+4 hidden modules”这个位置，不需要久等，直接Ctrl+C终止程序进行下面的配置即可。

3.Scratch-Blocks的配置
cd ../scratch-blocks
npm install
npm link

4.Scratch-GUI的配置
cd ../scratch-gui
npm install
npm link scratch-vm scratch-blocks
npm install
npm start

5.打开浏览器，在地址栏中输入 0.0.0.0:8061即可访问Scratch-Blocks，即Scratch 3.0界面。

![](/assets/anlione-ten.png)



