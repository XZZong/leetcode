#### 问题描述
对一个全部由‘0’和‘1’组成的二维数组，找到全部由‘1’组成的矩形（或正方形）的面积的最大值。

#### 自己的解题思路
1. 对于矩形：找到每个‘1’它的右边连续‘1’的个数，再遍历一遍数组，计算每个可能的矩形的面积，找到最大的。
```c
int width = array[i][j];
while(i + temp < matrix.length && matrix[i + temp][j] == '1') {
    if(array[i + temp][j] < width)
        width = array[i + temp][j];
    temp++;
    if(width * temp > max)
        max = width * temp;
}
```
2. 对于正方形：如果当前所在位置（i，j）为‘1’，找到它右边和下面连续‘1’的长度，将边长sideLen初始为两种中的较小的。接下来对其他所有位置进行判断，确定是否都是‘1’，并对边长进行调整。
```c
 for (; x < sideLen; x++) {
    for (y = 1; y < sideLen; y++) {
        if (matrix[i + x][j + y] == '0') {           
            sideLen = y; // 边长调整
            x--;
            break;
        }
    }
} 
```

#### 好的解题思路
1. 两个题目都可以用动态规划进行求解
2. 对于矩形：还没看太懂，晚点在写
1. 对于正方形：dp[i][j]表示的是以（i，j）为右下角的正方形的边长。dp[i][j] = min(dp[i-1][j],dp[i][j-1],dp[i-1][j-1])+1。i=0，dp的取值就是数组的第一行；j=0，dp的取值就是数组的第一列。可以对过程进行优化，只使用一维数组存放中间结果。
```c
for (int j = 0; j < n; j++) {
    for (int i = 1; i <= m; i++) {
        int temp = dp[i];
        if (matrix[i - 1][j] == '1') {
            dp[i] = min(dp[i], min(dp[i - 1], pre)) + 1;
            sz = max(sz, dp[i]);
        } else {
            dp[i] = 0;
        }
        pre = temp;
    }
}
```
1. 自己对于动态规划只是知道思想，具体用来解决问题，很明显的，自己会用，但大多数自己都没有想到这个方法。对于有些问题，自己感觉可以用，但写不出状态转移函数。
