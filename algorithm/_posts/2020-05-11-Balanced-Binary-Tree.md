---
layout: post
title: Sword to Offer-55.2 平衡二叉树 ❀❀
---

* 题目描述：  
统计一个数字在排序数组中出现的次数。 

## 解题思路：

递归求子树深度，两边深度差小于等于1判定为平衡二叉树。

## AC代码：

```java
// Judge If Is a Balance Binary Tree

public class Solution {
    private boolean isBalance = true;
    
    public boolean IsBalanced_Solution(TreeNode root) {
        calculateHeight(root);
        return isBalance;
    }
    
    private int calculateHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = calculateHeight(root.left);
        int right = calculateHeight(root.right);
        if (Math.abs(left-right) > 1) {
            isBalance = false;
        }
        return 1 + Math.max(left, right);
    }
}
```

## 补充说明：  

* 注意：`isBalance`方法返回的`int`值只是为了递归流程，判断二叉树是否平衡的参数是`isBalance`。
  
* 这里是[牛客编码链接](https://www.nowcoder.com/practice/8b3b95850edb4115918ecebdf1b4d222?tpId=13&&tqId=11192&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)