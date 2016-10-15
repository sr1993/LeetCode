### 题目链接:
[Container With Most Water][1]


### 整体思想:
题意为从左到右排列着一些有高度的竖线，相邻竖线之间是等距的，当然它们的下端点都在同一水平面上，从里面
任意挑出两条竖线，将它们和水平面看做一个可以盛水的容器，问这些竖线最多可以盛多少水（也就是求两条竖线
可构成矩形的面积），不能倾斜容器。

我们从中可以得出一些结论：任意两条竖线都能构成一个容器，所以每一种情况（[l, r] 表示选取的两条竖线在l位置
和r位置上，0 <= l < r < n , n为竖线的条数）都需要考虑到；如果选定了两条竖线，那么盛水的多少（矩形的面积和
较短的那条竖线有很大关系，面积等于较短竖线的高度乘以两条竖线之间的距离。

O(n^2)复杂度的方法是很容易想到的，但我们要以O(n)的复杂度解决该问题。O(n^2)的方法时间多用在了每种情况
都要计算，可不可以在计算一种情况的前提下，有一些情况就不用计算了。方法为设置两个指针，l, r，分别代表选
取的两条直线。令l = 0, r = n - 1,即最外层的两条直线，可以得出一个矩形的面积area[l, r] 假设 l 是较短的那条直线，
那么我们仔细想想，有一些情况就不用再算了，该些情况是area[l, k] ,其中 l < k < r，因为这些情况的area[l, k]一定
是小于area[l,r]的，[l, r]是最外层，矩形的底边也就是r - l 是最大的，而且高度为l竖线的高度，而其它情况area[l, k]，
矩形底边k - l  <  r - l , 而且高度要小于等于l,所以area[l, k]这些情况就不用计算了。接下来的工作就是更新 l 和 r，从
前面可得知，更新r（较长的竖线)是没有用的，不用计算那些情况了，所以我们要移动的是较短的那条竖线，即 l++，
就得到了一种新的状态。前面假设的是l是较短的那条，如果r是较短的那条的话，同理，area[k, r]，l < k < r这些情况
就不用再计算了，更新操作为r--。当得到新的l 和 r后，重复前面的操作，直到 l == r 时就可以停止算法，得出答案。

对上面的算法进行总结：
①设置两个指针 l = 0, r = n - 1
②计算出一个面积area, 并判断是否更新该area(题目要求取最大的面积）
③寻找较短的那条竖线，如果是 l , 则执行 l++，如果是r，则执行 r--
④如果l == r，算法结束，否则跳到②

参考：
[Editorial Solution][2]
[An easy way to understand the algorithm][3]

### 参考代码1:
```java
public class Solution {
    public int maxArea(int[] height) {
        int len = height.length;
        int ans = 0;
        int l = 0, r = len - 1;//左右指针
        while(l < r){
        	ans = Math.max(ans, Math.min(height[l], height[r]) * (r - l));
        	if(height[l] < height[r]){
        		l++;
        	}else{
        		r--;
        	}
        }
        return ans;
    }
}
```


  [1]:https://leetcode.com/problems/container-with-most-water/
  [2]: https://leetcode.com/articles/container-most-water/
  [3]: https://discuss.leetcode.com/topic/3462/yet-another-way-to-see-what-happens-in-the-o-n-algorithm