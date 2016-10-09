# Lab1:DOL配置
---
##1.DOL框架描述
&emsp;&emsp;DOL(分布式操作系统)是一组独立软件通过网络沟通，且在物理上独立的计算节点，由三部分组成：

####1.DOL应用编程界面
&emsp;&emsp;DOL定义了一系列的计算和应用路径，从而在SHAPES平台上实现分布式的编程。通过这些路径，应用开发者们在对下层架构不甚了解的情况下也能进行编程。

####2.DOL模拟功能
&emsp;&emsp;为了能让开发者们能够测试他们的应用，DOL提供了功能模拟架构。除了功能上的测试，它还可以用于收集应用层面上的参数。

###3.DOL配对优化
&emsp;&emsp;DOL配对优化的目标在于整合应用的一系列优化方案。首先，基于XML的评估标准会抽象地描述应用和结构，接下来，所有信息都会被精确地在实际运行中得以展现。
##2.DOL安装笔记
#####1.安装一些必要的环境(ubuntu为例)：

`$	sudo apt-get update`

`$	sudo apt-get install ant`

`$ 	sudo apt-get install openjdk-7-jdk`

`$	sudo apt-get install unzip`

#####2.下载文件
`sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz`

`sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip`

#####3.解压文件
新建dol的文件夹 

`$	mkdir dol`

将dolethz.zip解压到 dol文件夹中

`$	unzip dol_ethz.zip -d dol`

解压systemc

`$	tar -zxvf systemc-2.3.1.tgz`

#####4.编译systemc
解压后进入systemc-2.3.1的目录下

`$	cd systemc-2.3.1`

新建一个临时文件夹objdir

`$	mkdir objdir`

进入该文件夹objdir

`$	cd objdir`

运行configure(能根据系统的环境设置一下参数，用于编译)

`$	../configure CXX=g++ --disable-async-updates`

运行效果如下

![img1](http://i.imgur.com/DrUMlnv.png)

编译

`$	sudo make install`

编译完后文件目录如下`$ cd ..        $ ls`

![img2](http://i.imgur.com/kneya9M.png)

####5.编译dol
进入刚刚dol的文件夹

`$	cd ../dol`
修改build_zip.xml文件
找到下面这段话，就是说上面编译的systemc位置在哪里，
`<property name="systemc.inc" value="YYY/include"/>`
`<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>`
把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）

然后是编译
`$	ant -f build_zip.xml all`

若成功会显示build successful


![img3](http://i.imgur.com/M7lTVzl.png)

接着可以试试运行第一个例子,进入build/bin/mian路径下

`$	cd build/bin/main`
然后运行第一个例子

`$	ant -f runexample.xml -Dnumber=1`

成功结果如图

![img4](http://i.imgur.com/4I8LB6Q.png)

##3.心得体会

在撰写Readme时，一开始在编译器中无法查看上传的图像，后来突然又全部出现，估计是网速或者验证的时间问题。