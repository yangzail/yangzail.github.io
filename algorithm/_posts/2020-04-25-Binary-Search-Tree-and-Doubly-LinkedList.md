---
layout: post
title: Sword to Offer-36 二叉搜索树与双向链表 ❀❀
---

* 题目描述：  
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。  

## 解题思路：

中序遍历二叉搜索树问题：  
1、使用一个`pre`指针记录上一个遍历到的`pNode`，并在每次遍历时修改双向指针，每次遍历后`pre`指向`pNode`，而`pNode`按照中序遍历指向下一个遍历的值；  
2、注意对于第一个`pNode`，其`pre`为`null`，是不需要进行双向指针设置的；  
3、遍历的第一个结点就是该返回的双向链表的表头元素，记得记录下并返回。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-36.png">
</center>


## AC代码：

```java
// Deep Copy A LinkedList with Random Area

public class Solution {
    private TreeNode head = null;
    private TreeNode pre = null;
    
    public TreeNode Convert(TreeNode pRootOfTree) {
        turnToList(pRootOfTree);
        return head;
    }
    
    private void turnToList(TreeNode pNode) {
        if (pNode == null) {
            return;
        }
        turnToList(pNode.left);  //最左元素是第一个元素
        
        if (head == null) {
            head = pNode;
        }
        if (pre != null) {
            pNode.left = pre;
            pre.right = pNode;
        }
        //回溯
        pre = pNode;
        turnToList(pNode.right);
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5?tpId=13&&tqId=11179&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)