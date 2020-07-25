---
layout: post
title: Sword to Offer-26 树的子结构 ❀❀
---

* 题目描述：  
输入两棵二叉树`A`，`B`，判断`B`是不是`A`的子结构。  
约定空树不是任意一个树的子结构。


## 解题思路：

递归调用：  
1、`HasSubtree`方法：  
若树`root1`有一个子树是`root2`，分为两种情况，树`root1`就是（`is`）树`root2`或者树`root1`的左右子树中包含（`has`）树`root2`，建立递归调用，返回`false`条件为树`root1`或者树`root2`为`null`（题目规定空树不为任何树的子结构）。  
2、`isSubTree`方法：  
若`root2`为`null`，表示树`root2`匹配完毕返回`true`；  
若`root2`不为`null`时`root1`为`null`，表示匹配失败返回`false`；  
若本次对比的两结点`value`不相等，表示两树不匹配，返回`false`；  
若`root1`和`root2`都不为`null`，且本次对比的两结点`value`也相等，进入递归进行子树的对比。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-26.png">
</center>


## AC代码：

```java
// Whether Tree root2 Is A SubTree of Tree root1

public class Solution {
    public boolean HasSubtree(TreeNode root1,TreeNode root2) {
        if (root1==null || root2==null) {
            return false;
        }
        return isSubtree(root1, root2) || HasSubtree(root1.left, root2) 
            || HasSubtree(root1.right, root2);
    }
    
    private boolean isSubtree(TreeNode root1, TreeNode root2) {
        //对比结束，匹配成功
        if (root2 == null) {
            return true;
        }
        //树root2该结点不为null，树root1该结点为null
        if (root1 == null) {
            return false;
        }
        //本次对比的结点值不相等
        if (root1.val != root2.val) {
            return false;
        }
        //本次对比的结点值相等，其左右子树都相同才能匹配成功
        return isSubtree(root1.left, root2.left) && isSubtree(root1.right, root2.right);
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6e196c44c7004d15b1610b9afca8bd88?tpId=13&&tqId=11170&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)