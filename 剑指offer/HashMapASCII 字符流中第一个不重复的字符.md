### HashMap/ASCII 字符流中第一个不重复的字符

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

```java
//	faster solution
//	we know that length of charstream is between 0-255 
//	so char[256] is better than HashMap
//  13% faster.
public class Solution {
    //Insert one char from stringstream
    private StringBuilder sc = new StringBuilder();
    char[] bitCal = new char[256];
    public void Insert(char ch)
    {
        bitCal[ch]++;
        sc.append(ch);
    }
  //return the first appearence once char in current stringstream
    public char FirstAppearingOnce()
    {
        String str = sc.toString();
        for(int i=0;i<str.length();i++){
            if(bitCal[str.charAt(i)]==1) return str.charAt(i);
        }
        return '#';
    }
}
```



```java
//normal HashMap put() containsKey() 
import java.util.Map;
import java.util.HashMap;
public class Solution {
    //Insert one char from stringstream
    private StringBuilder sc = new StringBuilder();
    Map<Character,Integer> cache = new HashMap<Character,Integer>();
    public void Insert(char ch)
    {
        if(!cache.containsKey(ch)){
            cache.put(ch,1);
        }
        else {
            cache.put(ch,cache.get(ch)+1);
        }
        sc.append(ch);
    }
  //return the first appearence once char in current stringstream
    public char FirstAppearingOnce()
    {
        String input = sc.toString();
        for(int i=0;i<input.length();i++){
            if(cache.get(sc.charAt(i))==1) return sc.charAt(i);
        }
        return '#';
    }
}
```

