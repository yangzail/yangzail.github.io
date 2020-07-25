---
layout: post
title: Sword to Offer-28 对称的二叉树 ❀❀
---

* 题目描述：  
请实现一个函数，用来判断一棵二叉树是不是对称的。  
注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。


## 解题思路：

递归调用：  
1、`isSymmetrical`方法用于判断某树root是否为镜像树，需满足条件为，左右子树互为镜像；  
2、重载`isSymmetircal`方法,设定两个参数`left`和`right`，判断两棵子树是不是互为镜像；  
3、两个参数的`isSymmerical`方法判定规则为：  
* 对比结点同时为`null`，返回`true`；  
* 对比结点中只有一个为`null`，返回`false`；
* 对比结点的`value`不相等时，返回`false`；
* 若两个结点都不为`null`，且`value`相等，说明这两个结点满足互为镜像，即子树的根互为镜像，接下来递归调用，判断两个结点的左右子树是否互为镜像；
* 规则为：  
* `left`结点的左子树应与`right`结点的右子树`value`相等；  
* `left`结点的右子树应与`right`结点的左子树`value`相等。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-28.png">
</center>


## AC代码：

```java
// Whether Binary Tree Is Symmerical

public class Solution {
    boolean isSymmetrical(TreeNode pRoot)
    {
        if (pRoot == null) {
            return true;
        }
        return isSymmetrical(pRoot.left, pRoot.right);
    }
    
    boolean isSymmetrical(TreeNode left, TreeNode right) {
        //判断结束会同时没有左右孩子
        if (left==null && right==null) {
            return true;
        }
        //如果root只有一个孩子（不同时为空，且有一个为空）
        if (left==null || right==null) {
            return false;
        }
        //如果左右孩子不相等已经可以判断不为镜像树了
        if (left.val != right.val) {
            return false;
        }
        //左右孩子相等还要判断子树的左右孩子依次递归
        return isSymmetrical(left.left, right.right) && 
            isSymmetrical(right.left, left.right);
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/ff05d44dfdb04e1d83bdbdab320efbcb?tpId=13&&tqId=11211&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)