---
layout: post
title: Sword to Offer-24 反转链表 ❀
---

* 题目描述：  
输入一个链表，反转链表后，输出新链表的表头。


## 解题思路：

头插法：  
建立一个头结点指向新链表用于返回，将原链表中的元素依次连接到头结点后面，注意连接顺序即可。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-24.png">
</center>


## AC代码：

```java
// Reverse The Linklist (Head Insertion)

public class Solution {
    public ListNode ReverseList(ListNode head) {
        if (head==null || head.next==null) {
            return head;
        }
        //新的链表
        ListNode newList = new ListNode(-1);
        ListNode pNode = head; //当前处理的结点
        while (pNode != null) {
            ListNode pNext = pNode.next;
            //注意下两句顺序，写反了就是死循环
            pNode.next = newList.next;
            newList.next = pNode;
            pNode = pNext;
        }
        return newList.next;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca?tpId=13&&tqId=11168&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)