### 题目链接:
[First Unique Character in a String][1]


  [1]:https://leetcode.com/problems/first-unique-character-in-a-string/
### 整体思想:
给定一个只有包含小写字母的字符串，求在字符串中只出现一次且下标最小的字母的下标，如果不存在，
就返回-1。Map记录每个字母出现的次数，遍历字符串，只要当前字符在Map中记录的次数为1，该字符
的下标就是答案。
### 参考代码:
```java
public class Solution {
    public int firstUniqChar(String s) {
		int ans = -1;
		Map<Character,Integer> map = new HashMap<>();//字符和该字符出现的次数
		int len = s.length();
		
		for(int i = 0; i < len; ++ i){
			if(map.get(s.charAt(i)) == null){
				map.put(s.charAt(i), 1);
			}else{
				int cnt = map.get(s.charAt(i));
				map.put(s.charAt(i), ++ cnt);
			}
			
		}
		
		for(int i = 0; i < len; ++ i){
			if(map.get(s.charAt(i)) == 1){
				ans = i;
				break;
			}
		}
		
        return ans;
    }
}

```