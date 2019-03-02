3. (HARD)Longest Substring Without Repeating Characters ()

   quite classic, using:  HashMap method get()  、two pointers

   Main solution: 

   - every loop update max with two pointers (i-j+1) or remain max

3. ```java
   Given a string, find the length of the longest substring without repeating characters.
   Input: "abcabcbb"
   Output: 3 
   Explanation: The answer is "abc", with the length of 3. 
   
   
   class Solution {
       public int lengthOfLongestSubstring(String s) {
           HashMap<Character,Integer> Mapj = new HashMap<Character,Integer>();
           int max=0;
           for(int i=0,j=0;i<s.length();i++){
               if(Mapj.containsKey(s.charAt(i))){
                   j=Math.max(Mapj.get(s.charAt(i))+1,j);
               }
               Mapj.put(s.charAt(i),i);
               max = Math.max(max,i-j+1);
           }
           return max;
       }
   }
   ```
