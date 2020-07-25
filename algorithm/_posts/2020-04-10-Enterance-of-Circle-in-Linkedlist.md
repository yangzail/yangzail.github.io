---
layout: post
title: Sword to Offer-23 链表中环的入口结点 ❀
---

* 题目描述：  
给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出`null`。


## 解题思路：

主要是数学原理:  
1、设置快慢指针，假如有环，他们最后一定相遇;  
2、两个指针分别从链表头和相遇点继续出发，每次走一步，最后一定相遇与环入口。  
证明如下：
设链表头到环入口长度为--`a`    
环入口到相遇点长度为--`b`  
相遇点到环入口长度为--`c`  
则：  
相遇时, 快指针路程 = `a+(b+c)k+b` ，`k>=1`,   
其中`b+c`为环的长度，`k`为绕环的圈数,`k>=1`即最少一圈，不能是`0`圈;  
慢指针路程 = `a+b`;    
快指针走的路程是慢指针的两倍，所以`（a+b）*2=a+(b+c)k+b`,  
化简得`a=(k-1)(b+c)+c`,这个式子的意思是:  
链表头到环入口的距离 = 相遇点到环入口的距离 + `(k-1) *` 圈环长度;  
其中`k>=1`,所以`k-1>=0`圈;  
所以两个指针分别从链表头和相遇点出发,最后一定相遇于环入口。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-23.png">
</center>


## AC代码：

```java
// Find The Enterence of Circle in A Linklist

public class Solution {
    public ListNode EntryNodeOfLoop(ListNode pHead)
    {
        if (pHead==null || pHead.next==null) {
            return null;
        }
        ListNode p1 = pHead;
        ListNode p2 = pHead;
        do {
            p1 = p1.next;
            p2 = p2.next.next;
        }
        while (p1 != p2);
        p1 = pHead;
        while (p1 != p2) {
            p1 = p1.next;
            p2 = p2.next;
        }
        return p1;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/253d2c59ec3e4bc68da16833f79a38e4?tpId=13&&tqId=11208&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)