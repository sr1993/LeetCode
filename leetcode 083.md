### 题目链接:
[Remove Duplicates from Sorted List][1]


  [1]:https://leetcode.com/problems/remove-duplicates-from-sorted-list/
### 整体思想:
在节点元素排好序的链表中，去掉重复的元素。

### 参考代码:
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null){
        	return null;
        }
        ListNode pre  = head;
        ListNode cur = head.next;
        while(cur != null){
        	if(cur.val == pre.val){
        		if(cur.next == null){//当前是最后一个节点
        			pre.next = null;
        			cur = pre.next;
        		}else{//不是最后一个，断链，重连
        			pre.next = cur.next;
        			cur = pre.next;
        		}
        	}
        	else{
        		pre = cur;
        		cur = cur.next;
        	}
        }
        return head;
    }
}
```