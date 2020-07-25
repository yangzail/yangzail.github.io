---
layout: post
title: Sword to Offer-32.2 把二叉树打印成多行 ❀❀
---

* 题目描述：  
从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

## 解题思路：

外循环条件为队列不空，使用一个`size`保存每次内循环开始时的队列长度，即每一层结点个数，内循环条件为`size`不为`0`，完成将队列中结点出队并将结点值添加到`list`中，同时将这些结点的孩子入队，最后`size--`，每次内循环结束时，要将`list`添加到`ret`中（`ret`为`ArrayList`的`ArrayList`），最终返回`ret`；  

层次遍历参见[32.1](https://yangzail.github.io/algorithm/2020-04-19-Print-Binary-Tree-From-Left-to-Right/)。


## AC代码：

```java
// Hierarchical Traverse Binary Tree And Print With Lines

import java.util.ArrayList;
import java.util.Deque;
import java.util.LinkedList;

public class Solution {
    ArrayList<ArrayList<Integer> > Print(TreeNode pRoot) {
        ArrayList<ArrayList<Integer> > ret = new ArrayList<>();
        Deque<TreeNode> deque = new LinkedList<>();
        if (pRoot == null) {
            return ret;
        }
        deque.add(pRoot);
        
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
            ret.add(list);
        }
        return ret;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/445c44d982d04483b04a54f298796288?tpId=13&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)