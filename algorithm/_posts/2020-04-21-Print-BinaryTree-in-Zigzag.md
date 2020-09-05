---
layout: post
title: Sword to Offer-32.3 按之字形顺序打印二叉树 ❀❀
---

* 题目描述：  
请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。  

## 解题思路：

为层次遍历按行输出的程序添加隔行翻转,使用一个参数表示奇偶行，是偶数行的时候翻转`list`即可；  

层次遍历按行输出参见[32.2](https://yangzail.github.io/algorithm/2020-04-20-Print-Binary-Tree-In-Lines/)。


## AC代码：

```java
// Hierarchical Traverse Binary Tree And Print With Zigzag Lines

import java.util.ArrayList;
import java.util.Deque;
import java.util.LinkedList;
import java.util.Collections;

public class Solution {
    public ArrayList<ArrayList<Integer> > Print(TreeNode pRoot) {
        ArrayList<ArrayList<Integer> > ret = new ArrayList<>();
        Deque<TreeNode> deque = new LinkedList<TreeNode>();
        if (pRoot == null) {
            return ret;
        }
        
        deque.add(pRoot);
        boolean isOdd = false;
        while (!deque.isEmpty()) {
            ArrayList<Integer> list = new ArrayList<>();
            int size = deque.size();
            while (size > 0) {
                TreeNode pNode = deque.pop();
                list.add(pNode.val);
                if (pNode.left != null) {
                    deque.add(pNode.left);
                }
                if (pNode.right != null) {
                    deque.add(pNode.right);
                }
                size--;
            }
            if (isOdd) {
                Collections.reverse(list);
            }
            if (!list.isEmpty()) {
                ret.add(list);
            }
            isOdd = !isOdd;
        }
        return ret;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/91b69814117f4e8097390d107d2efbe0?tpId=13&&tqId=11212&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)