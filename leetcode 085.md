### 题目链接:
[Maximal Rectangle][1]


### 整体思想:
这道题是[Largest Rectangle in Histogram][2]的应用，是在该基础上的一个包装。在该矩阵中，每次遍历一行，
在遍历该行的时候，把改行以下的部分都忽略掉，那么该行以及以上的部分就构成了前面问题的一个模型，可
以说是一模一样的。在构造模型的时候要注意，如果该第i行的第j列是'0',那么该模型该列的直方图的高度为0，
如果第j列是'1'，则用原来模型该列的高度+1得到新模型该列直方图的高度。对于每一个模型，都运用前面问题
的算法，就可以得到整个问题的解。

### 参考代码:
```java
public class Solution {
    public int maximalRectangle(char[][] matrix) {
        int m = matrix.length;//行数
        //数组为空的情况
        if(matrix == null || matrix.length == 0
        		|| (matrix.length == 1 && matrix[0].length == 0))
        	return 0;
        
        int n = matrix[0].length;//列数
        int h[] = new int[n + 1];//高度数组
        int ans = 0;
        
        for(int i = 0; i < m; ++i){//遍历每一行，构造一个新的模型
        	for(int j = 0; j < n; ++j){
        		if(i == 0){
        			h[j] = matrix[i][j] - '0';
        		}else{
        			h[j] = matrix[i][j] == '0' ? 0 : h[j] + 1;
        		}
        	}
        	//构造好了模型
        	Stack<Integer> s = new Stack<Integer>();
        	for(int j = 0; j <= n; ++j){
        		while(!s.empty() && h[j] < h[s.peek()]){
        			int height = h[s.peek()];
        			s.pop();
        			int width = s.empty() ? j : (j - s.peek() - 1);
        			if(ans < height * width){
        				ans = height * width;
        			}
        		}
        		s.push(j);
        	}
        }
       
        return ans;
    }
}
```


  [1]:https://leetcode.com/problems/maximal-rectangle/
  [2]: https://github.com/sr1993/LeetCode/blob/master/leetcode%20084.md