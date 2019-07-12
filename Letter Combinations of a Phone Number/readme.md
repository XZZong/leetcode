### 问题描述
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.  
A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.  
String[] mapping = new String[] {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};  
Input: "23"  
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

### 解题思路
输入的数字为a1a2a3...an，前k个数字的映射结果存放在List中  
可以通过前K个数的映射结果，计算前k+1个数的（FIFO）  
1. 找到a(k+1) 对应的字符串s
1. 获取List头部的字符串（移除式获取）
1. 将上面的字符串与字符串s的每个字符的和加入到List中
1. 当List[0]的长度为k+1时，前k+1个数的映射结果就得到了

这个方法也可以应用到求一个集合的所有子集，不同的是原来的List保留  
以集合｛1,2,3,4｝为例，给出每一步的结果  
{""}  
{""} + {1} = {"", 1}  
{"", 1} + {2, 12} = {"", 1, 2, 12}  
{"", 1, 2, 12} + {3, 13, 23, 123} = {"", 1, 2, 12, 3, 13, 23, 123}  
{"", 1, 2, 12, 3, 13, 23, 123} + {4, 14, 24, 124, 34, 134, 234, 1234} = {"", 1, 2, 12, 3, 13, 23, 123, 4, 14, 24, 124, 34, 134, 234, 1234}
