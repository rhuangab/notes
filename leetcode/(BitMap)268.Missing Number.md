268. Missing Number

     Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

```java
class Solution {
	//using a single int array index to store a number is in or not
	//can be fast in small case.
    public int missingNumber(int[] nums) {
        int[] cache = new int[nums.length+1];
        for(int i=0;i<nums.length;i++)cache[nums[i]]++;
        for(int i=0;i<cache.length;i++){
            if(cache[i]==0) return i;
        }
        return 0;
    }
}
```

```java
//bitMap: each bits of the elements of the int array
//long time coding
//faster than java JDK func BitSet
class Solution {
    public int missingNumber(int[] nums) {
    	//initialize bitMap array
        int[] cache = new int[1+nums.length+1/32];
        //index: the offset bits(<=32)
        int temp = 0, index = 0;
        for(int i = 0;i < nums.length ; i++){
            //calculate the offset
            index = nums[i]%32;
            //set the bit from 0 to 1 by only one bit calculation
            cache[nums[i]/32] |= (1<<index);
            temp = 0;
        }
        for(int i=0;i<cache.length;i++){
            temp = cache[i];
            for(int j=0;j<=31;j++){
                //check the bit by only one bit calculation
                if((temp&(1<<j))==0) return i*32+j;
            }
        }
    return 0;
    }
}
```

```java
//BitSet: Short time coding
//time cost more than the int array bitmap
class Solution {
    public int missingNumber(int[] nums) {
        BitSet bit = new BitSet(nums.length+1);
        for(int i=0;i<nums.length;i++)
            bit.set(nums[i]);
        for(int i=0;i<nums.length+1;i++){
            if(!bit.get(i)) return i;
        }
        return 0;
    }
}	
```

