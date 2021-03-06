#### 问题描述
计算二叉完全树的节点个数

#### 我的解题思路
因为完全树的性质，我决定找到完全树的最后一个节点在树的最后一行是第几个，从而计算出完全树的节点个数。但在查找的时候存在回退，整个过程非常耗时，导致没有通过。整个题目花了很久，最后决定看discuss。

#### 好的解题方法
1. 完全树的根节点的子树也是完全树。如果根节点的右子树的树高与整棵树的树高相差为1，那么，最后的节点在右子树上，左子树是一棵完全树；否则，右子树就是一棵完全树。
height(root.right) == h-1 ? (1 << h) + countNodes(root.right) : (1 << h-1) + countNodes(root.left);（本来是2^n - 1，加上根节点就是2^n）
这里的树高是从0开始的。
1. 定义left和right两个指针，left一直往左移动（left=left.left），right一直往右移动，直到right=null。此时，如果left也为null，那么这棵树是一棵满二叉树，直接输出(1 << height) - 1；否则，输出1 + countNodes(root.left) + countNodes(root.right)。整个算法的时间复杂度为O(log(n)^2)，因为左子树和右子树至少有一个是满二叉树
