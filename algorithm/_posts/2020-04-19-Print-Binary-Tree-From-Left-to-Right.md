---
layout: post
title: Sword to Offer-32.1 从上往下打印二叉树 ❀❀
---

* 题目描述：  
从上往下打印出二叉树的每个结点，同层结点从左至右打印。  

## 解题思路：

二叉树的层次遍历：  
1、利用队列保存根节点；  
2、只要队列不为空，每出队一个结点，将该结点的左右孩子依次入队（如果存在），从而完成从上到下从，左到右的层次遍历。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-32.1.png">
</center>


## AC代码：

```java
// Hierarchical Traversal of Binary Tree

import java.util.ArrayList;
import java.util.Deque;
import java.util.LinkedList;

public class Solution {
    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<>();
        if (root == null) {
            return list;
        }
        Deque<TreeNode> deque = new LinkedList<>();
        
        deque.add(root);
        while (!deque.isEmpty()) {
            TreeNode pNode = deque.poll();
            list.add(pNode.val);
            if (pNode.left != null) {
                deque.add(pNode.left);
            }
            if (pNode.right != null) {
                deque.add(pNode.right);
            }
        }
        return list;
    }
}
```

## 补充说明：
* 补充：
`Deque`双向队列是`Queue`单向队列的子类，`Deque`是抽象类，其实现有`ArrayDeque`和`LinkedList`。`Deque`用法非常灵活：  
1、首先可以用作队列：  
`add(e)`等效于`addLast(e)`;  
`offer(e)`等效于`offerLast(e)`;  
`remove()`等效于`removeFirst()`;  
`poll()`等效于`pollFirst()`;  
`element()`等效于`getFirst()`;  
`peek()`等效于`peekFirst()`。  
2、实际上还可用作堆栈：  
`push(e)`等效于`addFirst(e)`;  
`pop()`等效于`removeFirst()`;    
`peek()`等效于`peekFirst()`。  


* 这里是[牛客编码链接](https://www.nowcoder.com/practice/7fe2212963db4790b57431d9ed259701?tpId=13&&tqId=11175&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)