### 题目链接:
[Valid Parentheses][1]


### 整体思想:
括号匹配问题，用栈解决。

### 参考代码1:
```java
public class Solution {
    public boolean isValid(String s) {
        int len = s.length();
        if(len % 2 != 0 || len == 0){
        	return false;
        }
        Stack<Character> st = new Stack<Character>();
        for(int i = 0; i < len; i++){
        	char c = s.charAt(i);
        	if(!valid(c)){
        		return false;
        	}
        	if(st.isEmpty()){
        		st.push(c);
        	}else{
        		char top = st.peek();
        		if(top == '['){
        			if(c == ']')
        				st.pop();
        			else
        				st.push(c);
        		}else if(top == '{'){
        			if(c == '}')
        				st.pop();
        			else
        				st.push(c);
        		}else if(top == '('){
        			if(c == ')')
        				st.pop();
        			else
        				st.push(c);
        		}
        	}
        }
         if(st.isEmpty())
        	return true;
        else
        	return false;
    }
    
	public boolean valid(char c){
		if(c != '[' && c != ']' && c != '(' && c != ')'
				&& c != '{' && c != '}')
			return false;
		return true;
	}
}
```


  [1]:https://leetcode.com/problems/valid-parentheses/