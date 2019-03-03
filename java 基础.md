# java 基础

### 关键字

#### 1.final
- 对于数据：final使数据不变

* 对于引用：不可以改变引用的对象（地址）
* 对于方法：声明方法不能被子类重写

- - - -
#### 2.static

* 静态变量：又称为类变量，也就是说这个变量属于类的，类所有的实例都共享静态变量，可以直接通过类名来访问它。静态变量在内存中只存在一份。
* 实例变量：每创建一个实例就会产生一个实例变量，它与该实例同生共死




###  String 

#### String Pool（String的不变性）

 **String Pool:** 在Java虚拟机（JVM）中存在着一个字符串池，其中保存着很多String对象，并且可以被共享使用，因此它提高了效率。由于String类是final的，它的值一经创建就不可改变，因此我们不用担心String对象共享而带来程序的混乱。

注：在 Java 7 之前，String Pool 被放在运行时常量池中，它属于永久代。而在 Java 7，String Pool 被移到堆中。这是因为永久代的空间有限，在大量使用字符串的场景下会导致 OutOfMemoryError 错误。

- intern()方法

  调用intern()方法，常量池内若存在当前句柄字符串，则返回该字符串的引用。否则，在常量池内添加该字符串并返回添加字符串的引用

  - 何时会向常量池中存储字符串对象：
    - 显式调用String的intern方法时 //String str = new String("aa").intern();
    - 直接声明字符串字面量时 // String str = "aa";
    - 字符串字面量相加时 //String str = "aa"+"bb";

  ```java
  //public String intern() 
  //Returns a canonical representation for the string object.
  String temp = "hh";
  s1 = "a" + temp;
  // 如果调用s1.intern 则最终返回true
  s2 = "ahh";
  System.out.println(s1 == s2);    // false
  ```

  因此，初始化String时，最好用字面量创建字符串，方便直接用常量池中取出使用

- 

- 以new String("2222") 创建字符串 会生成两个对象

` String s1 = new String("2222")`  

#### String 拼接

String str = "aa"+"bb"; //这一段代码在jdk1.8中，会被编译器自动优化，即字面量提前合成为"aabb"然后再

//

------

### ArrayList

ArrayList实现了List接口，实现了动态数组，约等于C++的Vector，但它不是线程安全的，在多线程环境下改变ArrayList结构必须注意同步**（synchronized）**

#### contains()

contains()与HashMap的containsKey相比，效率低很多，因为contains()会遍历整个数组，复杂度有O(n)，而HashMap散列key的方法，主要的开销在遍历散列的拉链，复杂度为O(1)

------

### AOP (Aspect Oriented Programming)

AOP：面向切面编程，是OOP的一种补充。OOP引入封装、继承、多态等概念来建立对象机制，纵向地关注核心功能（如业务处理过程），AOP则收集横向的、分布在核心关注点附近、与业务功能无关的、但为业务模块所共同调用的逻辑或责任封装起来的代码。

AOP把软件系统分为两部分：核心关注点和横切关注点

### IOC(Inverse Of Control)

IOC为相互依赖的组件提供抽象，通过依赖注入的方式进行控制反转。

比如：各个类之间存在耦合关系，那么只要将底层类作为参数传入上层类的构造函数，需要作出修改的时候只要修改底层类即可。其实这也是一种解耦的过程。

依赖注入的方式需要大量的new实例，可以使用**控制反转容器**IOC container进行自动new。

- 只需要维护一个configuration，而不用每次都new那么多实例
- 直接隐藏具体的创建实例的细节

------



### 类加载

#### 类内部加载顺序

- 类加载时，先加载内部static代码块。

- 构造代码块：在类中单独的语句块{ }，将在该语句块所在类构造函数内执行且首先执行

#### Class.forName()

Class.forName(String className)保证了一个类被加载，而new实例的类不一定。

Class.forNme(String className)实际上把new实例过程解耦，第一步加载类，第二步Class.forNme(String className).newInstance()



------

### 数组 Array

#### 多维数组初始化

- 直接赋值 ： `int a[][] = {{1,2},{3,4}};`

- 分别赋值：  `int [][] ints = new int[4][2]` 

- 第二维度动态申请空间： `int [][] arr3 = new int [5][];`

  进行赋值时，每次都要手动申请每个第二维元素的空间