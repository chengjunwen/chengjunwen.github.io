---
layout: post
title:  "二叉查找数/AVL树"
date:   2017-02-05 16:29:33 +0800
categories:
excerpt:
---

二叉查找树、平衡二叉查找树、红黑树、B树

#### 二叉查找树
二叉查找数是指排序之后的二叉树，具有以下性质

* 若任意节点的左子树不空，则左子树上所有结点的值均小于它的根结点的值；  
* 若任意节点的右子树不空，则右子树上所有结点的值均大于它的根结点的值；  
* 任意节点的左、右子树也分别为二叉查找树；  
* 没有键值相等的节点（no duplicate nodes）；    

![BinaryTree](/home/cjw/image/binarytree/binarytreesearch.png)
如果节点数是n个，二叉查找树的查找时间复杂度一般为 O(log(n))，最坏的情况下可能是O(n)  

#### 平衡二叉平衡查找树(AVL tree)
&emsp;由于二叉查找树可能退化成链表，时间复杂度变成O(n)(此时树的深度是 n ),为了解决这一问题，产生了平衡二叉树。  
&emsp;平衡二叉查找数引入了平衡的概念，相对于二叉查找树，多了一个限制条件： 对于每一个节点，它的左右子树的深度之差不能超过 1 。当在插入或者删除元素时，可能会破坏上面那个规则，这个时候可以通过节点旋转将二叉树再次平衡。平衡二叉树的平衡性质将树的查找删除等操作的时间复杂度很好的稳定在O(log(n)),不会出现一般二叉树的最坏情况，不过平衡二叉树的旋转操作也会消耗时间O(log(n))  
![BalanceBinaryTree](/home/cjw/image/binarytree/balanceTree.jpg)

##### 失衡调整
**平衡二叉树的失衡调整是通过旋转最小失衡子树来完成的**

##### 左旋： left rotation
当新插入节点在右子树的右节点上时，需要进行左旋，**找到距离插入节点最近的一个不平衡节点(调整最小失衡子树)**，将该节点向左边旋转：  
![](/home/cjw/image/binarytree/leftRotation.jpg)  
![](/home/cjw/image/binarytree/leftRotationEg.jpg)

##### 右旋： right rotation
当新插入节点在左子树的左节点上时，需要进行左旋，**找到距离插入节点最近的一个不平衡节点**，将该节点向右边旋转：  
![](/home/cjw/image/binarytree/rightRotation.jpg)  
![](/home/cjw/image/binarytree/rightRotationEg.jpg)  

##### 先左旋再右旋： left-right rotation
当新插入节点在左子树的右节点上时，需要先进行左旋再右边旋转，**找到距离插入节点最近的一个不平衡节点**，先将该节点的左子节点左旋，再将该节点向右边旋转：   
![](/home/cjw/image/binarytree/left_right.jpg)  

##### 先右旋再左旋： right-left rotation
当新插入节点在右子树的左节点上时，需要先进行右旋再左旋，**找到距离插入节点最近的一个不平衡节点**，先将该节点的右子节点右旋，再将该节点向左边旋转：  
![](/home/cjw/image/binarytree/right_left.jpg)  


#### 红黑树
红黑数，也是一种二叉查找树，满足一般二叉查找树的所有性质,对二叉树进行着色和规定以下一些性质，也可以将树维持在平衡状态：

* 每个结点要么是红的要么是黑的；  
* 根结点是黑的；  
* 每个叶结点（叶结点即指树尾端NIL指针或NULL结点）都是黑的；  
* 如果一个结点是红的，那么它的两个儿子都是黑的；  
* 对于任意结点而言，其到叶结点树尾端NIL指针的每条路径都包含相同数目的黑结点；  

![RedBlackTree](/home/cjw/image/binarytree/redblacktree.png)  

#### B-tree

B-tree 是为磁盘等存储设备设计的一种多叉平衡查找树，每个节点有多个分支。  
与其他二叉树不同的是，B-Tree的一个节点包含有多个(t)关键码，根据t个关键码，其子节点就有 t+1 个，例如有3个关键字的节点有4个字节点，关于一个 m 阶的B-Tree有以下性质（m>=2）：

1. 每个节点至多有 m 个字节点  
2. 除了根节点，其他分支节点至少有 ceil(m/2)个子节点（向上取整）, 根据 1，2两个性质，可以发现每个节点(根节点除外)的关键字t范围是 $$$ceil(m/2)-1<=t<=m-1$$$  
3. 根节点至少有两个子节点（或者该树只有一个根节点）  
4. 所有的叶子节点都在同一层上  
5. 有 j 个子节点的非叶子节点有 j-1个关键码，且关键码按照升序排序  

![](/home/cjw/image/binarytree/B-tree.jpg)  

![](/home/cjw/image/binarytree/B-TreeEg.jpg)



























