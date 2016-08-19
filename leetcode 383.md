### 题目链接:
[Ransom Note][1]


  [1]: https://leetcode.com/problems/ransom-note/
### 整体思想:
两个字符串，均只包含小写字母，问用后者字符串的所有字母（每个字母只能用1次），能否组成前面的字符串。
比如ab  和 bcad，是可以的，而aaab 和  daab不可以，因为后者只有两个a。因为小写字母只有26个，所以开辟
两个26空间大小的两个数组，分别保存各自每个字母出现的次数，要满足条件，只要每个字母后者出现的次数大
于或等于前者出现次数就可以了。
### 参考代码:
```java
public class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        long[] ori = new long[26];
        long[] now = new long[26];
        boolean ok = true;
        for(int i = 0; i < magazine.length(); i ++){
            ori[magazine.charAt(i) - 'a'] ++;
        }
        for(int i = 0; i < ransomNote.length(); i ++){
        	now[ransomNote.charAt(i) - 'a']++;
        }
        for(int i = 0; i < 26; i ++){
        	if(now[i] > 0 && ori[i] < now[i])
        	{
        		ok = false;
        		break;
        	}
        }
        return ok;
    }
}
```
