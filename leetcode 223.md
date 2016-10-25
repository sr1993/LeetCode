### 题目链接:
[Rectangle Area][1]


### 整体思想:
给定两个矩形，左上角和右上角点的坐标已经给定。求这两个矩形覆盖的面积。分两种情况，一种是两个矩形不相交，则
覆盖面积为两个矩形的面积和，另一种情况是两个矩形相交，则所求面积为两个矩形面积的和减去相交的面积，这里要注
意一个矩形可能为一个点，或者一条直线，要特殊判断一下。

### 参考代码1:
```java
public class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        //两个矩形不相交，或者有矩形是一条直线或一个点
		int total = (C - A) * (D - B) + (G - E) * (H - F);
		if(E >= C || A >= G || B >= H || F >= D || A == C || B == D || E == G || F == H){
			return total;
		}
		//总面积-交叉的面积（交叉面积的长等于小的右边界-大的左边界， 宽等于小的上边界-大的下边界）
		return total - (Math.min(C, G) - Math.max(A, E)) * (Math.min(D, H) - Math.max(B, F));
    }
}
```


  [1]:https://leetcode.com/problems/rectangle-area/