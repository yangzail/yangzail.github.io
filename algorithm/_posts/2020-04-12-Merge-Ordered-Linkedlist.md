---
layout: post
title: Sword to Offer-25 合并两个排序的链表 ❀
---

* 题目描述：  
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。


## 解题思路：

归并排序法的归并部分：  
新建一个链表的头结点用于返回，定义两个指针指向两个`list`的开头，将较小的值放入新链表末尾，遍历直至某个`list`遍历完成，最后将可能没有遍历完成的那个链表直接接到新链表末尾。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-25.png">
</center>


## AC代码：

```java
// Merged Two linkedList

public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        ListNode head = new ListNode(-1);
        ListNode pNode = head;
        while (list1!=null && list2!=null) {
            if (list1.val <= list2.val) {
                pNode.next = list1;
                list1 = list1.next;
            }
            else {
                pNode.next = list2;
                list2 = list2.next;
            }
            pNode = pNode.next;
        }
        if (list1 != null) {
            pNode.next = list1;
        }
        if (list2 != null) {
            pNode.next = list2;
        }
        return head.next;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337?tpId=13&&tqId=11169&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)