---
layout: post
title: Sword to Offer-22 链表中倒数第k个结点 ❀
---

* 题目描述：  
输入一个链表，输出该链表中倒数第`k`个结点。


## 解题思路：

1、设置一个指针`p2`从头开始先走k步，之后设置另一个指针`p1`从头开始与`p2`一起向后移动，那么当`p2`走到链表尽头为`null`的时候`p1`恰好指向倒数第`k`个结点;    
2、注意考虑特殊情况，`p2`走完`k`步已经走出了链表，说明链表元素不足`k`个，无不存在倒数第`k`个结点，直接返回`false`。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-22.png">
</center>


## AC代码：

```java
// Find the Last k-th Number in Linklist

public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if (head == null) {
            return null;
        }
        ListNode p1 = head;
        ListNode p2 = head;
        //p1指向表头，p2指向p1后面第k个元素
        while (p2!=null && k!=0) {
            p2 = p2.next;
            k--;
        }
        //p2还没有走k步就已经遍历完了链表，此时不存在倒数第k个结点
        if (k > 0) {
            return null;
        }
        //当p2走到表尾，p1就是倒数第k个元素
        while (p2 != null) {
            p1 = p1.next;
            p2 = p2.next;
        }
        return p1;
    }
}
```

## 补充说明：
* 注意：若`p2`到链表最后一个结点就停下，往前数`k`个结点`p1`指向倒数第`k+1`个结点，所以需要等`p2`指向`null`时停止循环。  

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/beb5aa231adc45b2a5dcc5b62c93f593?tpId=13&&tqId=11166&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)