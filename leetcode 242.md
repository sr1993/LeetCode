### 题目链接:
[Valid Anagram][1]


  [1]:https://leetcode.com/problems/valid-anagram/
### 整体思想:
判断一个字符串与另一个字符串相比，是否是包含相同字符，可以顺序不一样，比如adac 和 daac就
满足。将字符串转化为数组，然后排序，遍历一下就可以了，如果当前位置二者的字符不同，那么肯
定不是符合条件的。

### 参考代码:
```java
public class Solution {
    public boolean isAnagram(String s, String t) {
		int lenS = s.length();
		int lenT = t.length();
		if(lenS != lenT){
			return false;
		}
		
        char[] S = s.toCharArray();
        char[] T = t.toCharArray();
        Arrays.sort(S);
        Arrays.sort(T);
        
        boolean ans = true;
        for(int i = 0; i < lenS; ++i){
        	if(S[i] != T[i]){
        		ans = false;
        		break;
        	}
        }
        
        return ans;
    }
}

```