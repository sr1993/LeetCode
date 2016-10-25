### 题目链接:
[Add Strings][1]


### 整体思想:
两个大数以字符串的形式给出，求两个数的和。从两个字符串的末尾开始，模拟数字相加，同时处理即可。当一个数的数字
还有剩余时（另一个数的数字已经处理完），结果还要加上剩余的数字，另外格外要注意是否进1的标志位。

### 参考代码:
```java
public class Solution {
    public String addStrings(String num1, String num2) {
		if(num1.equals("") || num2.equals("")){
			return num1.equals("") ? num2 : num1;
		}
        String ans = "";
        int len1 = num1.length();
        int len2 = num2.length();
        len1--; 
        len2--;
        boolean flag = false;
        
        while(len1 != -1 && len2 != -1){    //注意是-1，不是0
        	int a = num1.charAt(len1) - '0';
        	int b = num2.charAt(len2) - '0';
        	int sum = a + b;
        	if(flag == true){
        		sum++;
        	}
        	if(sum > 9){
        		flag = true;
        		ans += Integer.toString(sum - 10);
        	}else{
        		flag = false;
        		ans += Integer.toString(sum);
        	}
        	len1--;
        	len2--;
        }
        
        while(len1 != -1){
        	int sum = (flag == true ? 1 : 0) + (num1.charAt(len1) - '0');
        	if(sum > 9){
        		flag = true;
        		ans += Integer.toString(sum - 10);
        	}else{
        		flag = false;
        		ans += Integer.toString(sum);
        	}
        	len1--;
        	
        }
        while(len2 != -1){
        	int sum = (flag == true ? 1 : 0) + (num2.charAt(len2) - '0');
        	if(sum > 9){
        		flag = true;
        		ans += Integer.toString(sum - 10);
        	}else{
        		flag = false;
        		ans += Integer.toString(sum);
        	}
        	len2--;
        }
        if(flag == true){
            ans += "1";
        }
        return new StringBuilder(ans).reverse().toString();
    }
}
```


  [1]:https://leetcode.com/problems/add-strings/