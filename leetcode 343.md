### 题目链接：
[Integer Break][1]
[1]: https://leetcode.com/problems/integer-break/
### 参考代码：
``` java
public class Solution {
    public int integerBreak(int n) {
        //总体思想就是把n分成尽相同的几个数，那么它们相乘起来才有可能值最大
        int ans = -1;
        if(n == 2)
        	return 1;
        for(int i = 1; i <= n - 1 ; i ++){//不能是数本身，所以 i 不能到 n
        	int times = n / i; //将n分成times个i, 比如当n = 10，i = 3时，times = 3, 也就是3+3+3+1,及3^3*1 ,1是余数
        	int left = n % i;//余数
        	int fac = 1;//计算阶层， 也就是i ^ times是多少，因为要乘起来
        	for(int k = 1; k <= times; ++k){
        		fac = fac * i;
        	}
        	
        	if(left != 0){
        		if(times > 2){//意思是，分成的数，至少有2个是相同的，times是i这个数出现的次数
        		    ans = Math.max(ans, fac * left);//这句和下面两句必须都写，两种情况
        		    ans = Math.max(ans, fac / i * (i + left));
        		    /*比如n= 10, n = 3+3+3+1，相乘起来即3^3*1=27,再比较将
        		    3个重复的3中取出一个，加到余数上，变成了3+3+4,乘起来3^2*4 = 36，是后者大
        		    还能举出一个例子，比如11， 分成 3+3+3+2, 3^3*2 = 54,取出一个3，加到余数上成了 3+3+5, 3^2*5 = 45,
        		    显然前者大，所以这两个比较缺一不可
        		    */
        		}
        		else//times = 1的情况，也就是比如11分成 10 + 1, 9 + 2, 8 + 3这样的，只能两个数相乘
        			ans = Math.max(ans, fac * left);
        	}
        	else{//余数等于0的情况，也就是times个i相乘，就是最大值，即上面算出的fac
        	    ans = Math.max(ans,  fac);
        	}
        		
        }
    	return ans;
    }
}
```
