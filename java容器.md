## java容器

### ArrayList

ArrayList实现了List接口，实现了动态数组，约等于C++的Vector，但它不是线程安全的，在多线程环境下改变ArrayList结构必须注意同步**（synchronized）**

#### contains()

contains()与HashMap的containsKey相比，效率低很多，因为contains()会遍历整个数组，复杂度达到了O(n)，而HashMap散列key的方法，主要的开销在遍历散列后bucket里的拉链，复杂度为O(1)

#### 两个ArrayList 大小比较并更换引用

比如若要比较两个ArrayList的大小，可以交换互相的引用变量

```
ArrayList<Integer> cache1 = new ArrayList<Integer>();
ArrayList<Integer> cache2 = new ArrayList<Integer>();
cache1.add(1);
cache2.add(1);
cache2.add(2);
/*	exchange reference
	After comparation, cache1.size()>cache2.size()
*/
if(cache1.size()<cache2.size()){
            ArrayList<Integer> temp = cache1;
            cache1 = cache2;
            cache2 = temp;
        }
```



### HashMap

```java
HashMap<K,V> map  = new HashMap<K,V>();	
```

HashMap：key-value模式，key、value都必须为类，基本数据类型需要声明成包装类，put的时候传入基本数据类型会自动打包。



### StringBuffer

StringBuffer 继承自AbstractStringBuilder ，而这个抽象类中有值得注意的地方：

- 另一个 int count  指的是目前已被用到的char数组（这里count必须小于value.length() ），但是count是AbstractStringBuilder的方法的返回值 

- ```java
  abstract class AbstractStringBuilder implements Appendable, CharSequence {
      /**
       * The value is used for character storage.
       */
      char[] value;
      /**
       * The count is the number of characters used.
       */
      int count;
      /**
       * Returns the current capacity. The capacity is the amount of storage
       * available for newly inserted characters, beyond which an allocation
       * will occur.
       * @return  the current capacity
       */
  	public int length(){
     		return count;
  	}
  }
  ```

  也就是说，平时StringBuilder StringBuffer 的方法length.()返回的是已被插入的新char 而不是capacity。

  capacity是AbstractStringBuilder底层char数组的大小，当length()达到capacity时，就需要复制数组并扩容

