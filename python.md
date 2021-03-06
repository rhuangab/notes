#  python
## 折线图
``` 
import matplotlib.pyplot as plt
x=[0,1,2,3,4,5,6,7,8,9]
y=[0,0.824,0.867,0.872,0.925,0.931,0.948,0.952,0.952,0.957]
plt.figure(figsize=(10,1)) ## 创建figure
plt.plot(x,y,linewidth=3,color='r',marker='o') ## 设置xy轴
plt.xlabel("loop(s)") 
plt.ylabel("Accuracy")
#修改坐标刻度
plt.xticks(np.linspace(1,14,14))
plt.yticks(np.linspace(0.07,0.12,25))
plt.title("Accuracy During nine loops")
plt.show()
```

------

## 程序入口

 if __name__ == "__main__" :

而Python属于脚本语言，不像编译型语言那样先将程序编译成二进制再运行，而是动态的逐行解释运行。也就是从脚本第一行开始运行，没有统一的入口。

一个 Python 源码文件除了可以被直接运行外，还可以作为模块（也就是库）被导入。不管是导入还是直接运行，最顶层的代码都会被运行（**Python 用缩进来区分代码层次**）。而实际上在导入的时候，有一部分代码我们是不希望被运行的。

`if __name__ == '__main__'` 就相当于是 Python 模拟的程序入口。Python 本身并没有规定这么写，这只是一种编码习惯。**由于模块之间相互引用，不同模块可能都有main的定义，而入口程序只能有一个。**到底哪个入口程序被选中，这取决于 `__name__` 的值。

------

## xrange与range的区别

range()返回的是一个list 

xrange()是调用一次就返回一次值

python 3.x 中xrange与range的实现已经相同

------

###**python语句**

以#开头的语句是注释，注释是给人看的，可以是任意内容，解释器会忽略掉注释。其他每一行都是一个语句。

当语句以冒号:结尾时，缩进的语句视为代码块。

Python程序是大小写敏感的，如果写错了大小写，程序会报错。

------

###**数据类型和变量**

在Python中，能够直接处理的数据类型有以下几种：整数、浮点数、字符串

####**浮点数**

但是对于很大或很小的浮点数，就必须用科学计数法表示，把10用e替代，1.23x109就是1.23e9

####**字符串**

字符串内部既包含'又包含"怎么办？可以用转义字符\来标识。

转义字符\可以转义很多字符，比如\n表示换行，\t表示制表符，字符\本身也要转义，所以\\\表示的字符就是\

