### container with most water

#### 问题描述
给你一个由非负数构成的数组，每个一个数表示坐标系中的一个点（i, ai）。那么坐标系中存在n条垂直于x轴的线段，任意两条线段和x轴组成一个容器。
寻找到容纳水最多的容器（木桶效应，容器的高取决于最短的那条边）
![picture](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

#### 解题思路
暴力的方法是把所有可能的都计算一遍，找到其中的最大值。但这种方法中有很多计算是多余的，下面以一个长度为6的数组进行说明：

一开始我们计算(1,6)这两个点的结果。假设点1更短，那么(1,2)、(1,3)、(1,4)、(1,5)都不需要计算。
因为它们组成的容器的最大高度与(1,6)相同，即线段1的长度，而它们的宽都比(1,6)小，所以它们组成的容器体积不可能超过(1,6)。

**因此我们只需要每次将两个边中较短的那条往另一边移动**，计算n-1次，就可以得到我们想要的结果。
```
                                x、-表示不需要计算
          1 2 3 4 5 6                1 2 3 4 5 6             1 2 3 4 5 6
        1 x ------- o              1 x ------- o           1 x ------- o
        2 x x                      2 x x       o           2 x x - o o o
        3 x x x                    3 x x x     |           3 x x x o | |
        4 x x x x                  4 x x x x   |           4 x x x x | |
        5 x x x x x                5 x x x x x |           5 x x x x x |
        6 x x x x x x              6 x x x x x x           6 x x x x x x         
```
### trapping rain water
#### 问题描述
给你一个由非负数构成的数组，数组中的每一个数表示坐标系中宽度为1高为该数的墙。计算可以容纳多少体积的水。
![picture](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

#### 解题思路
分别找到左边和右边的最大高度，并将它们记录下来。处理最大高度小的那边：累加。（我感觉自己说不清，结合一些图进行说明会更清楚吗？下面是别人自己的解释）
Search from left to right and maintain a max height of left and right separately, which is like a one-side wall of partial container. Fix the higher one and flow water from the lower part. For example, if current height of left is lower, we fill water in the left bin. Until left meets right, we filled the whole container.
