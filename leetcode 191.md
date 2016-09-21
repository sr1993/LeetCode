### 题目链接:
[Number of 1 Bits][1]


### 整体思想:
知识点：（来源于网络）
计算机对有符号数（包括浮点数）的表示有三种方法：原码、反码和补码， 补码=反码+1。在 二进制里，是用 0 和 1
来表示正负的，最高位为符号位，最高位为 1 代表负数，最高位为 0 代表正数。

以java中8位的byte为例，最大值为：0111 1111，最小值为1000 0001。
那么根据十进制的数字，我们如何转换为二进制呢？对于正数我们直接转换即可，对于负数则有一个过程。
以负数-5为例：
1.先将-5的绝对值转换成二进制，即为0000 0101；
2.然后求该二进制的反码，即为 1111 1010；
3.最后将反码加1，即为：1111 1011

所以Java中Integer.toBinaryString(-5)结果为11111111111111111111111111111011. Integer是32位(bit)的.

求一个数的二进制表示中‘1’的个数，该数要求被当做无符号数对待。可以一位一位的判断，也可以利用位运算跳跃判断。
### 参考代码1:
```java
public class Solution {
    public int hammingWeight(int n) {
		int ans = 0;
		
		while(n != 0){
			ans += n & 1;
			n >>>= 1;
		}
		
		return ans;
    }
        
}
```

### 参考代码2:
```java
public class Solution {
    public int hammingWeight(int n) {
		int ans = 0;
        
        while(n != 0){
            n = n & (n - 1);
            ans++;
        }
        
        return ans;
    }
}
```
  [1]:https://leetcode.com/problems/number-of-1-bits/