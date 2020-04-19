# Implementation of Priority Queue

Priority Queue/Heap 维护了一个每次poll都是最小元素。是用complete binary tree实现。

所谓的"完全二叉树", 要满足:

> * 除了最后一层, 所有层都排满\(没有非空节点\)
> * 最后一层的所有非空节点都排在左边

一张图可以直观说明, 完全二叉树其实就是长得像这样:  
![](http://x-wei.github.io/images/heap-summary/pasted_image.png)  


root节点总是最小值，因此 peek\(\): 返回数组的第一个元素的值，时间复杂度O\(1\)。所以获得最小值的时间复杂度为O\(1\).

  
poll\(\): 拿出数组的第一个元素，heap中剩下的元素要进行调整，保证heap是min heap的结构，这个过程是heapifyDown。

heapifyDown: 把最后一个元素放到root的位置，从root位置开始，比较root位置代表的parent与其左右children的大小，parent总是与children中元素较小的进行交换。 重复这个过程，直到大的元素不再有children。时间复杂度是O\(lgn\)。

  
Insert\(\): 插入一个新的元素，总是放在数组元素的最后一个位置，然后heapifyUp，调整heap满足min heap。

heapifyUp: 数组新增的最后一个元素与其parent进行比较， 如果新增元素的值小于其parent的值，则进行交换，递归此过程。时间复杂度是O\(lgn\)。

build树的时候，因为有n个node，每加入一个都要heapify，所以时间复杂度是O\(nlgn\)





  


  
  


