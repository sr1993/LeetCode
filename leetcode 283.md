### 题目链接:
[Move Zeroes][1]


  [1]:https://leetcode.com/problems/move-zeroes/
### 整体思想:
将一个整型数组中的0移到数组的末尾，其它位置数字的相对位置保持不变。扫描一遍，记录0出现
的个数，边扫描边移动数字，最后将0补到末尾。

### 参考代码:
```java
public class Solution {
    public void moveZeroes(int[] nums) {
	      int k = 0;//0出现的个数
	      int len = nums.length;
	      
	      for(int i = 0; i < len; ++i){
	    	  if(nums[i] == 0){
	    		  ++k;
	    	  }else{
	    		  nums[i - k] = nums[i];
	    	  }
	      }
	      
	      for(int i = len - k; i < len; ++i){
	    	  nums[i] = 0;
	      }
	}
}

```