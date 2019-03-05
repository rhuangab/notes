Two Sum

```java
//两层循环，一层用于往HashMap put 另一层查找
//the order of the put is (num[i],i) 
//the first position apply for comparing
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int res[] = new int[2];
        HashMap<Integer,Integer> m = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            m.put(nums[i],i);
        }
        for(int i=0;i<nums.length;i++){
            int t = target-nums[i];
            if(m.containsKey(t)&&m.get(t)!=i){
                res[0]=i;
                res[1]=m.get(t);
                break;
            }
        }
        return res;
    }
}

//the second method is 20% faster
//using only one loop and less compares
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int res[] = new int[2];
        HashMap<Integer,Integer> m = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            int t = target-nums[i];
            if(m.containsKey(t)){
                res[0]=i;
                res[1]=m.get(t);
                break;
            }
            m.put(nums[i],i);
        }
        return res;
    }
}
```

