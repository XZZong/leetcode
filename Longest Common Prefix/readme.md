### 问题描述
Write a function to find the longest common prefix string amongst an array of strings.
If there is no common prefix, return an empty string ""  
给你一组字符串，找到它们的公共前缀，没有就返回空串

### 解题思路
1. 一个一个地比较  
初始化公共前缀pre为第一个字符串，在后续字符串中判断pre是否为它们的前缀，如果不是，就不断地删除pre的最后一个字符，直到新的pre是该字符串的前缀
1. 找到最大的和最小的字符串  
discussion有这样一个方法，对所有字符串进行排序，然后找到最小字符串和最大字符串的公共前缀，就是想要的答案。
评论中说不需要排序，因为排序的目的就是找到最大的和最小的字符串，只需要遍历一次数组就可以得到结果。  
我发现String类存在函数compareTo（String），满足进行字符串比较的要求，就根据整数数组找最大数和最小数的方法改写了算法，结果还行。  

这里的问题是方法2虽然只是遍历了一次数组，进行了3/2*n次比较，但compareTo函数的时间跟字符串的长度有关，不一定占优势
