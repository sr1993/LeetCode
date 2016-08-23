### 题目链接:
[Longest Palindromic Substring][1]


  [1]:https://leetcode.com/problems/longest-palindromic-substring/
### 整体思想:
求一个字符串的最长回文子串。采用复杂度为O(n)的Manacher算法，将原串cdadcbcdad处理成
$#c#d#a#d#c#b#c#d#a#d#^，然后运用Manacher算法。
### 参考代码:
```java
public class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        char[] ma = new char[len * 2 + 3];
        int[] pArr = new int[len * 2 + 3];
        int pR = 0, index = 0;
        //处理原字符串
        len = 0;
        ma[len ++] = '$';
        ma[len ++] = '#';
        for(int i = 0; i < s.length(); ++ i){
        	ma[len ++] = s.charAt(i);
        	ma[len ++] = '#';
        }
        ma[len ++] = '^';
        int maxLen = -1;
        pArr[0] = 1;
        int L = 0, R = 0;//答案的指针
        for(int i = 1; i < len - 1; ++ i){
        	pArr[i] = pR > i ? Math.min(pArr[2 * index - i], pR - i) : 1;
        	while(ma[i + pArr[i]] == ma[i - pArr[i]]){
        		++ pArr[i];
        	}
        	if(i + pArr[i] > pR){
        		pR = i + pArr[i];
        		index = i;
        	}
        	if(maxLen < pArr[i] - 1){
        		maxLen = pArr[i] - 1;
        		R = i + pArr[i] - 2;
        		L = i - pArr[i] + 2;
        	}
        }
        
        String ans = s.substring(L / 2 - 1, R / 2);
        return ans;
    }
}

```