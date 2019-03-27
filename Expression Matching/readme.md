#### 正则表达式

'.'表示任意字符，'*'表示上一个字符重复任意次

这里的方法是使用一个动态规划进行求解，规则如下
- p.charAt(j) == s.charAt(i)
  
  dp[i][j] = dp[i-1][j-1]
- p.charAt(j) == '.'
  
  dp[i][j] = dp[i-1][j-1]
- p.charAt(j) == '*'
  1. p.charAt(j-1) != s.charAt(i) 
     
     dp[i][j] = dp[i][j-2]   //in this case, a* only counts as empty
  1. p.charAt(i-1) == s.charAt(i) or p.charAt(i-1) == '.'
       
       dp[i][j] = dp[i-1][j]    //in this case, a* counts as multiple a 

    or dp[i][j] = dp[i][j-1]   // in this case, a* counts as single a
    
    or dp[i][j] = dp[i][j-2]   // in this case, a* counts as empty
