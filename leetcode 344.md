### 题目链接:
[Reverse String][1]


  [1]: https://leetcode.com/problems/reverse-string/
### 整体思想:
使用Java中StringBuffer的函数。
### 参考代码:
```java
public class Solution {
    public String reverseString(String s) {
        return new StringBuffer(s).reverse().toString();
    }
}
```