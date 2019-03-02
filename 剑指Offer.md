### 剑指Offer

#### 和为S的连续正数序列

```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer> > result = new ArrayList<ArrayList<Integer> >();
        //return special case
        if(sum==1) {
            return result;
        }
        int i=1;
        while(i<sum){
           //right index means the next add number
           //left index means the first number of the sequence
            
           int cacheSum = 0; 
           int leftIndex = i;
           int rightIndex = i;
           while(true){
               if(cacheSum<sum) {
                   cacheSum+=rightIndex;
                   rightIndex++;
                   continue;
               }
               else if(cacheSum>sum){
                   cacheSum-=leftIndex;
                   leftIndex++;
               }
               else if(cacheSum == sum){
                   if(leftIndex==rightIndex-1) break;
                   ArrayList<Integer> subResult = new ArrayList<Integer>();
                   for(int p=leftIndex;p<rightIndex;p++){
                       subResult.add(p);
                   }
                   result.add(subResult);
                   break;
               }
           }
            i = leftIndex+1;
       }
        return result;
    }
}
```

