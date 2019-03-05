771. Jewels and Stones

使用HashMap，空间换时间，查询对比即可

You're given strings `J` representing the types of stones that are jewels, and `S` representing the stones you have.  Each character in `S` is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in `J` are guaranteed distinct, and all characters in `J` and `S`are letters. Letters are case sensitive, so `"a"` is considered a different type of stone from `"A"`.

```java
class Solution {
    public int numJewelsInStones(String J, String S) {
        int count = 0;
        HashMap mapJ = new HashMap();
        for(int i = 0; i<J.length(); i++) 
            mapJ.put(J.charAt(i),i);
        for(int i = 0; i<S.length(); i++){ 
                if(mapJ.containsKey(S.charAt(i)))
                    count++;
            }
        return count;
    }
        
}
```

