#### 问题描述
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.  
将K个已排好序的数组整合为一个数组

#### 解题思路
点赞最好的方法使用的是优先队列  
优先队列是一种用来维护一组元素构成的结合S的数据结构，其中每个元素都有一个关键字key，元素之间的比较都是通过key来比较的。
优先队列的实现中，可以选择堆数据结构

如果理解为，往优先队列中加入头节点时，它原有的后继节点都看作左孩子，是把它当作别的节点的右孩子或别的节点当它的右孩子。
这样似乎可以明白为什么代码中加入的只是头节点，而在不断poll（取优先队列的头节点）的过程中，可以遍历到所有的节点。

我的做法是不断进行两两归并。在这个过程中，每循环一次，需要进行两两归并的数组个数减少一倍。
有人和我的想法类似，（我一开始的步长为2/n，逐渐减小为1，所有的结果都放在了list的前几项中，需要同时修改数组长度和步长；
他一开始的步长为1，逐渐增加到n，只需要修改步长即可），
但时间上比我短。（是因为他在进行两两归并时，如果一个为null直接返回另一个，这步处理导致的吗？）  

```java
int step = 1;
while(step < lists.length){
    for(int i = 0; i +step< lists.length;i = i+step*2){
        lists[i] = mergeTwoLists(lists[i],lists[i+step]);
    }
    step *=2;
}
---------------------------------------------
int d = (length + 1) / 2;
while (length > 1) {
    for(int i = 0; i + d < length; i++) {
        lists[i] = merge(lists[i], lists[i + d]);
    }
    length = d;
    d = (d + 1) / 2;
}
```
