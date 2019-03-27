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



#### 用两个栈来实现一个队列

```java
public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
    }
    
    public int pop() {
        //clear stack2 first
        if(!stack2.empty())
            return stack2.pop();
        else {
            //if stack2 is empty, then transfer whole stack1 to stack2
            if(stack1.empty()) return -1; //in case of empty queue 
            while(!stack1.empty())
            stack2.push(stack1.pop());
        }
         return stack2.pop();   
    }
}		
```



#### 斐波拉契数列

```
public class Solution {
    public int Fibonacci(int n) {
        int a=1,b=1,fib=0;
        if(n<0)return 0;
        if(n==1||n==2)return 1;
        else{
        	//Using recursive way costs much.
        	//increase the n linearly, the fib(1) operands increases exponentially.
        	//Using iteration can acclerate the former addition with linear time complexity
            for (int i=3;i<=n;i++){
                fib=a+b;
                a = b;
                b = fib;
            }
        }
        return fib;
    }
}
```

合并两个排序的链表

```java


public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
    	//in case of null input
        if(list1==null&&list2==null) return null;
        //result iterates to the end of the List
        //ans is the return variable
        ListNode result = new ListNode(2);
        ListNode ans = result;
        while(list1!=null||list2!=null){
            //none null case
            if(list1!=null&&list2!=null){
                if(list1.val<=list2.val){
                    result.val = list1.val;
                    list1 = list1.next;
                }
                else{
                    result.val = list2.val;
                    list2 = list2.next;
                }
            }
            //single null case, directly link the rest of the listNode
            //sdecrease 50% time cost
            else{
                if(list1==null){
                    result.val = list2.val;
                    result.next = list2.next;
                    break;
                }
                else{
                    result.val = list1.val;
                    result.next= list1.next;
                    break;
                }
            }
            if(list1==null&&list2==null) break;
            ListNode cache = new ListNode(2);
            result.next = cache;
            result = result.next;
        }
        return ans;
    }
}
```

