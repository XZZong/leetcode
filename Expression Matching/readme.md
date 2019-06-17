#### 正则表达式
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

>'.' Matches any single character.  
'\*' Matches zero or more of the preceding element.  

The matching should cover the entire input string (not partial).

这里的方法是使用一个动态规划进行求解。整个状态表flag是 (s.length() + 1) * (p.length() + 1) 的，flag[i][j]表示的是s的前i个字符和p的前j个字符是否匹配
flag[0][0] = true

初始化：当s的长度为0时，p的p.charAt(j) j = 1,3,5,... 必须都是 '\*' 这样两者才算等价的

flag[0][j+1] = flag[0][j-1] if p.charAt(j) == '\*'

一般情况：
- 两个对应位置的字符相同，或者p所在位置的字符是'.', (p.charAt(j) == s.charAt(i) || p.charAt(j) == '.')

  dp[i][j] = dp[i-1][j-1]
  
- 当对应位置字符不同时，只需对p所在位置是'\*'的情况进行考虑，(p.charAt(j) == '\*')
  1. p.charAt(j-1) != s.charAt(i) && p.charAt(i-1) != '.'
     
     如果前一个字符不是'.'，且不与s的对应位置字符相同，那么这里的a* 只能匹配为空（自己复写的时候，没有注意到这一点，确实需要单独考虑）
     flag[i][j] = flag[i][j-2] 
  1. 其他       
          flag[i][j] = flag[i-1][j]    //in this case, a* counts as multiple a (关于这里的匹配多个，似懂非懂)

       or flag[i][j] = flag[i][j-1]   // in this case, a* counts as single a
    
       or flag[i][j] = flag[i][j-2]   // in this case, a* counts as empty
