### 题目链接:
[Path Sum][1]


### 整体思想:
给定二叉树，问从树根到叶子节点是否存在一条路径，使得节点值的和等于给定的值。采用递归，分别对左右子树
进行判断。如果成功，就返回true。
### 参考代码:
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
	public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null){//空树
            return false;
        }
        
		if(root.left == null && root.right == null){//叶子节点
			if(sum == root.val)
				return true;
			return false;
		}
		
		boolean l = false, r = false;//左子树是否满足条件，右子树同
		if(root.left != null){
			l = hasPathSum(root.left, sum - root.val);
		}
		
		if(l == true)
		    return true;
		
		if(root.right != null){
			r = hasPathSum(root.right, sum - root.val);
		}
		return l | r;//有一个满足条件就可以
    }
}
```
  [1]:https://leetcode.com/problems/path-sum/