#### 问题描述
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. 
If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.  
将给定的链表每k个进行一次反转，不足k个的不处理。

#### 解题思路
一种方法是使用递归，还有一种方法是先确定链表的长度，进而确定需要反转的次数。后一种方法空间复杂度为O(1)  

在链表前面进行元素添加，一般使用如下方法
```
n = head;
p = null;
for (int j = 0; j < k; j++) {
    ListNode next = n.next;
    n.next = p;
    p = n;
    n = next;
}
```
