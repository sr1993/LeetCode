### ��Ŀ���ӣ�
[Integer Break][1]

  [1]: https://leetcode.com/problems/integer-break/
  - - -
  ### �ο����룺

``` java
public class Solution {
    public int integerBreak(int n) {
        //����˼����ǰ�n�ֳɾ���ͬ�ļ���������ô��������������п���ֵ���
        int ans = -1;
        if(n == 2)
        	return 1;
        for(int i = 1; i <= n - 1 ; i ++){//���������������� i ���ܵ� n
        	int times = n / i; //��n�ֳ�times��i, ���統n = 10��i = 3ʱ��times = 3, Ҳ����3+3+3+1,��3^3*1 ,1������
        	int left = n % i;//����
        	int fac = 1;//����ײ㣬 Ҳ����i ^ times�Ƕ��٣���ΪҪ������
        	for(int k = 1; k <= times; ++k){
        		fac = fac * i;
        	}
        	
        	if(left != 0){
        		if(times > 2){//��˼�ǣ��ֳɵ�����������2������ͬ�ģ�times��i��������ֵĴ���
        		    ans = Math.max(ans, fac * left);//��������������붼д���������
        		    ans = Math.max(ans, fac / i * (i + left));
        		    /*����n= 10, n = 3+3+3+1�����������3^3*1=27,�ٱȽϽ�
        		    3���ظ���3��ȡ��һ�����ӵ������ϣ������3+3+4,������3^2*4 = 36���Ǻ��ߴ�
        		    ���ܾٳ�һ�����ӣ�����11�� �ֳ� 3+3+3+2, 3^3*2 = 54,ȡ��һ��3���ӵ������ϳ��� 3+3+5, 3^2*5 = 45,
        		    ��Ȼǰ�ߴ������������Ƚ�ȱһ����
        		    */
        		}
        		else//times = 1�������Ҳ���Ǳ���11�ֳ� 10 + 1, 9 + 2, 8 + 3�����ģ�ֻ�����������
        			ans = Math.max(ans, fac * left);
        	}
        	else{//��������0�������Ҳ����times��i��ˣ��������ֵ�������������fac
        	    ans = Math.max(ans,  fac);
        	}
        		
        }
    	return ans;
    }
}
```