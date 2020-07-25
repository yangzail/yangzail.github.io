---
layout: post
title: Sword to Offer-55.1 二叉树的深度 ❀
---

* 题目描述：  
输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

## 解题思路：

递归求解：  
1、递归返回条件为当前`root`为`null`，到达叶子结点，递归结束；  
2、当前`root`不为`0`的时候，深度为`子树最大深度+1`，子树最大深度为`max(子树深度，右子树深度)`。


## AC代码：

```java
// Depth of Binary Tree

public class Solution {
    public int TreeDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        else {
            return 1 + Math.max(TreeDepth(root.left), TreeDepth(root.right));
        }
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/435fb86331474282a3499955f0a41e8b?tpId=13&&tqId=11191&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)