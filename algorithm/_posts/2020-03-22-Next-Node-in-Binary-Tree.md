---
layout: post
title: Sword to Offer-08 二叉树的下一个结点 ❀❀
---

* 题目描述：给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。   

* 解释：每个`TreeNode`有一个值`val`和三个指针`left`,`right`,`next`分别指向左孩子，右孩子和父亲结点。

## 解题思路：

1、向下查找：如果`pNode`有右子树，将`pNode`视为一个子树的`root`，`Root->Right`下一个结点在其右子树中找，是右子树中序遍历的第一个结点，即最左边的结点；  
2、向上查找：如果`pNode`没有右子树，则将`pNode`的父亲结点视为一个子树的`root`，看`pNode`是父亲结点的左还是右孩子；  
（1）如果是父亲结点的左孩子，`Left->Root`下一个遍历的即为父亲结点；  
（2）如果是父亲结点的右孩子，说明以父亲结点为根的子树已经遍历完成，再往上走，看父亲结点是爷爷结点的左还是右孩子，以此类推直到到达`root`结点。  

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-08.png">
</center>


## AC代码：

```java
// Find the Next Treenode of a Binary Tree's Mid-order Traversal

public TreeLinkNode GetNext(TreeLinkNode pNode){
        // if node has right child,the next node is the right child's
        // leftest child or itself(when no left child)
        if (pNode.right != null) {
            TreeLinkNode tmpNode = pNode.right;
            while (tmpNode.left != null) {
                tmpNode = tmpNode.left;
            }
            return tmpNode;
        }

        // if the node is its father's left child,return its father
        // else find upper util the node is the root of a left tree
        while (pNode.next != null) {
            TreeLinkNode parentNode = pNode.next;
            if (pNode == parentNode.left) {
                return parentNode;
            }
            pNode = pNode.next;
        }
        
        // the node is the rightest node of a tree
        return null;
    }
```
## 补充说明：

* 注意: 两次查找都以初始的`pNode`为起点，所以第一次查找时不要改变`pNode`的初始值。
* 这里是[牛客编码链接](https://www.nowcoder.com/practice/9023a0c988684a53960365b889ceaf5e?tpId=13&tqId=11210&tPage=3&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)