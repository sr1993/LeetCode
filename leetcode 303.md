### 题目链接:
[Range Sum Query - Immutable][1]


  [1]: https://leetcode.com/problems/range-sum-query-immutable/
### 整体思想:
查询给定数组任意区间的和，只要维护前缀和就可以了。
### 参考代码:
```java
public class NumArray {
    int[] ans = new int[10010];
    public NumArray(int[] nums) {
        ans[0] = 0;
        int tp = 0;
        for(int i = 0; i < nums.length; ++i){
            tp = tp + nums[i];
            ans[i+1] = tp;
        }
    }

    public int sumRange(int i, int j) {
        int l = i + 1;
        int r = j + 1;
        return ans[r] - ans[l - 1];
    }
}

```