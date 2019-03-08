# JVM
## JVM 运行时数据区域
**java虚拟机在执行java程序时 会把所管理的内存分成若干个不同的数据区域**

- stack(栈区)：主要保存基本数据类型（char、byte、short、int、long、float、double、boolean）以及对象的引用，数据可以共享，速度仅次于寄存器(register)，快于堆
- heap(堆区)：用于存储对象

#### JVM 堆内存组成

JVM堆内存由Perm区和Heap区组成。Heap区主要包括了Young 区、Old 区。

- Young区中包括了Eden、S1、S2三部分。在经历Minor GC之后，多数对象都被销毁了，内存被回收，少数留下的对象会被复制到S1、S2中的一个。因此Minor GC主要由扫描Eden区和复制对象到Survivor区组成。
- **晋升**： 每经历一次Minor GC的过程，Survivor区幸存对象的年龄都会加一，当它超过预设值MaxTenuringThreshold时，这个对象就会从Survivor区被移动到Old区，这个过程称为晋升
- Old区主要是用Major GC方法
- 全部GC使用的方法为Full GC
- Mark：https://tech.meituan.com/2017/12/29/jvm-optimize.html 美团整理文档

#### GC算法

- Minor GC：分为扫描和复制两部分
  - 优点：内存
- Mark-Sweep：也被称为tracing garbage collector，因此它要把程序能直接、间接访问到的所有对象都标记一次，主要分为Mark和Sweep阶段
  - Mark是指将所有root 引用到的所有对象都mark为true（包括间接引用的对象）
  - Sweep是指将所有mark为True的对象改为False，否则就清除该对象
  - 优点：即使存在循环引用，Mark过程也可以完成
  - 缺点：
    1. 在Mark-Sweep算法运行时，正常的程序会被挂起
    2. 算法会产生内存碎片(Fragmentations)，也就意味着碎片化的内存无法被合理利用起来，这个时候如果进行压缩（compaction），其实也就是通过复制内存的思路完成Memory之后，我们才能有效地利用其中的空间 。（但是前面的复制算法也有缺点，那就是必须牺牲一大部分的内存用于空闲的两个Survivor区中的一个）