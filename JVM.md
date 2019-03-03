# JVM
## JVM 运行时数据区域
**java虚拟机在执行java程序时 会把所管理的内存分成若干个不同的数据区域**

- stack(栈区)：主要保存基本数据类型（char、byte、short、int、long、float、double、boolean）以及对象的引用，数据可以共享，速度仅次于寄存器(register)，快于堆
- heap(堆区)：用于存储对象