### 19. Remove Nth Node From End of List

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode firstRound =head, secondRound = head;
		int length = 0;
		//calculate the length of List
		while(firstRound!=null) {
			length++;
			firstRound = firstRound.next;
		}
		//the beginning Node case
		if(length==n) {
            head = secondRound.next;
            secondRound.next = null;
        }
		else {	
		//point to the Node before the removing Node
				for(int i =0;i<=length-n-1;i++) {
                    //iterate to length-n-1
					if(i == length-n-1) {
						if(n==1) secondRound.next=null;//the last Node case
						else secondRound.next = secondRound.next.next;
					}
					else secondRound = secondRound.next; 
					}
			  }
        return head;
    }
}
```

