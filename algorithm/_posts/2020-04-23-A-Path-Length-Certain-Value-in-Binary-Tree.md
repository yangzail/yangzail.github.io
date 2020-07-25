---
layout: post
title: Sword to Offer-34 二叉树中和为某一值的路径 ❀❀
---

* 题目描述：  
输入一颗二叉树的根节点和一个整数，按字典序打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。  

## 解题思路：

回溯法：  
1、从根路径开始，每经过一个结点，将其添加进`path`数组，并从`target`减去其值，直到到达叶子结点且此时`target`恰好为`0`，此时判断找到了一条符合要求的路径，将`path`存入`pathMatrix`，否则对根结点的左右子树继续进行递归求解；  
2、递归求解时，如果左右子树的查找都失败了，就将`root`从`path`中删除，回溯该路径。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-34.png">
</center>


## AC代码：

```java
// Find A Path A Certain Length from Root to Leaf in Binary Tree

import java.util.ArrayList;

public class Solution {
    private ArrayList<ArrayList<Integer>> pathMatrix = new ArrayList<>();
    
    public ArrayList<ArrayList<Integer>> FindPath(TreeNode root, int target) {
        backTracking(root, target, new ArrayList<>());
        return pathMatrix;
    }
    
    private void backTracking(TreeNode root, int target, ArrayList<Integer> path) {
        if (root == null) {
            return;
        }
        path.add(root.val);
        target -= root.val;
        if (target==0 && root.left==null && root.right==null) {
            pathMatrix.add(new ArrayList<Integer>(path));
        }
        else {
            backTracking(root.left, target, path);
            backTracking(root.right, target, path);
        }
        // 回溯，每当当前root下无法找到合适路径，将当前root从path删去
        path.remove(path.size() - 1);
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/b736e784e3e34731af99065031301bca?tpId=13&&tqId=11177&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)