---
layout: post
title: Sword to Offer-27 二叉树的镜像 ❀
---

* 题目描述：  
操作给定的二叉树，将其变换为源二叉树的镜像。


## 解题思路：

递归调用：  
建立`mirror`方法用于输出一棵树的镜像；  
1、交换结点左右子树；  
2、对结点左子树调用`mirror`；  
3、对结点右子树调用`mirror`；  
4、`mirror`退出条件为结点为`null`。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-27.png">
</center>


## AC代码：

```java
// Mirror A Binary Tree

public class Solution {
    public void Mirror(TreeNode root) {
        if (root == null) {
            return;
        }
        swap(root);
        Mirror(root.left);
        Mirror(root.right);
    }
    
    private void swap(TreeNode root) {
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
    }
} 
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/564f4c26aa584921bc75623e48ca3011?tpId=13&&tqId=11171&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)