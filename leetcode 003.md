### 题目链接:
[Longest Substring Without Repeating Characters][1]


  [1]:https://leetcode.com/problems/longest-substring-without-repeating-characters/
### 整体思想:
题意为求一个字符串中最长连续子序列，该子序列里面不包含重复的字符。用到了哈希思想和两个指针。
r右指针是连续递增扫描的，而l左指针是跳跃的，只考虑[l, r)这部分区间，如果当r指向的字符在[l, r)中出
现过的话，那么更新答案，且将l指针指向r字符在[l, r)出现的位置的下一个位置。比如acdefd,当l指向a，r
当前指向最后一个字母d时，那么更新答案后，l下一次指向的位置则是第一个d的下一个位置，也就是e位
置。具体参考下面代码，不懂的话用例子 abcabcbb模拟算一遍就明白了。
### 参考代码:
```java
public class Solution {
    	public int lengthOfLongestSubstring(String s) {
		int len = s.length();
		if(len == 0)
			return 0;
		
		int ans = 1;
		int l = 0, r = 1;//两个指针
		int[] has = new int[128];//每个字符是否出现过，下面过程中[l,r)区间的字符has值是1
		int[] lastPos = new int[128];//每个字符上一次出现的位置
		lastPos[(int)s.charAt(0)] = 0;//第一个字符上一次出现的位置是0
		has[(int)s.charAt(0)]++;//第一个字符出现过
		
		for(; r < len && l <= r && l < len; ){
			while(r < len && has[s.charAt(r)] != 1){//r指针指向的字符在[l,r)之间没出现过
				has[s.charAt(r)]++;//记录该字符已经出现
				lastPos[s.charAt(r)] = r;//该字符第一次出现的位置
				++r;
			}

			if(r == len)//r到头了，要更新答案
			{
				ans = Math.max(ans, r - l);
				break;
			}
            
			//r指针指向的字符在[l,r)之间出现过
			ans = Math.max(ans, r - l);//更新答案
			for(int k = l; k <= lastPos[(int)s.charAt(r)]; k++){
				has[(int)s.charAt(k)]--;//没用了，去掉，不在范围之内，看下面那个注释
			}
			l = lastPos[(int)s.charAt(r)] + 1;//调到当前字母上一次出现位置的下一个位置
		}
		
        return ans;
    }
}

```