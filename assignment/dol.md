#DOL实例运行实验
***
&emsp;&emsp;本次实验主要修改了DOL中的两个测试样例，并借助画图工具Graphviz将生成的.dot图转化为.png图。
##实验截图
![ex2](http://i.imgur.com/s0GRaj5.png)

example2.png

![ex1](http://i.imgur.com/LKR3iOM.png)

example1.png

##实验过程
###1.修改example2.xml
&emsp;&emsp;通过修改iterator的迭代次数，将N的值改为2，使square模块变成两个。

![exp2](http://i.imgur.com/sbWvFoZ.jpg)

结果截图：

![](http://i.imgur.com/mtssdvb.png)

###1.修改example1中的square.c
&emsp;&emsp;将平方改为立方

![exp1](http://i.imgur.com/v2n3eZy.jpg)

结果截图：

![](http://i.imgur.com/GPKb0JC.png)

##实验感想和心得
&emsp;&emsp;本次实验让我对DOL模块和通道之间的关系有了更深的理解，了解到了迭代通道带来的影响。
&emsp;&emsp;另外，在安装本次实验用到的Graphbiz时，我先采用了wget下载再解压安装的方法，然而步骤繁琐而且并没有将需要的库安好。后来改用apt-get命令后一步搞定了。看来以后安装工具时要优先考虑apt-get啊。