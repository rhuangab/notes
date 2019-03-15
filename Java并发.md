## Java并发

### Java并发和并行



### 线程共享变量可见性原理

- 线程的工作内存：由JMM抽象出的一种内存模型，同一进程下不同线程会有属于私人的本地内存区域。
  - 此时对于不同线程间的变量共享，java通常会在线程创建时复制一份共享变量的副本，若要对共享变量进行修改，就要通过副本复制到主存中
  - 共享变量的通信方式：JMM限制了线程之间直接通信，主要通过主存的副本进行通信

- 其他线程想要获得这个修改后的变量，要等到JMM控制的共享变量读、写结束后，再从主存中拷贝副本获取。（有点类似 数据库服务器读-写分库后，**主数据库负责写，多个从数据库负责读**，但是数据库的思路更高明，一旦单点故障，可以使某一从数据库升级为主数据库）

- 上面这个过程其实实现了可见性，可见性就是指一个线程对共享变量值的修改，能够及时地被其他线程看到。
  - 要实现可靠的可见性：除了正确进行共享变量的读、写方式，还需要在共享变量写之后及时的读取

### Synchronized代码块

```java
public class DDbug implements Runnable{
	public Integer a = new Integer(0);
	public void changeA() {
		try {
			synchronized(this.a) {
				System.out.println("线程："+Thread.currentThread().getName()+"准备进入同步块");
				System.out.println("线程："+Thread.currentThread().getName()+"准备退出同步块");
			}
			System.out.println("线程："+Thread.currentThread().getName()+"准备退出函数d");
		}
		catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
	public void changeB() {
		try {
            //synchronized block maintain the object inside bracket: 
            //		synchronized(object obj){}
            //if obj is changed during synchronized period, the synchronized cannot work
			synchronized (this.a) {
				a = new Integer(3);
				System.out.println("线程："+Thread.currentThread().getName()+"进入同步块中"+" a:"+this.a.intValue());
			}
		}
		catch (Exception e) {
			e.printStackTrace();
		}
	}
	public static void main(String[] args) throws InterruptedException {
		DDbug syn1 = new DDbug();
		Thread t1 = new Thread(new Runnable() {			
			@Override
			public void run() {
				syn1.changeA();
				
			}
		});
		Thread t2 = new Thread(new Runnable() {
			@Override
			public void run() {
				syn1.changeB();
			}
		});
		t1.start();
		Thread.sleep(200);
		t2.start();
	}
}
```

- synchronized方法锁住当前实例对象（即 this）
- synchroinzed代码块锁住的是传入的对象参数  synchroinzed(Object obj)
- 多线程环境下，要等已经运行到synchronized块的线程释放锁之后，才能再次给对象加锁。即使两个不同的代码段，都要锁同一个对象，那么这两个代码段也不能在多线程环境下同时运行
  - 全局锁：synchronized(className.class){} //这样的话可以锁住类的class对象

#### java三种高并发https://blog.csdn.net/java_xth/article/details/81162088

### 