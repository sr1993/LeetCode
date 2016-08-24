### 题目链接:
[Add Digits][1]


  [1]:https://leetcode.com/problems/add-digits/
### 整体思想:
一个整数执行这样的过程： 比如 129  → 1 + 2 + 9 = 12  → 1 + 2 = 3，相加直到最后是一位数为止，
返回它。用到了九余数定理，一个数对9取余等于该数各个数字相加之和对9取余。所以可以在O(1)
复杂度解决。

### 参考代码:
```java
public class Solution {
    public int addDigits(int num) {
		if(num == 0){
			return 0;
		}
		int left = num % 9;
		if(left == 0){
			return 9;
		}else{
			return left;
		}
	}
}

```