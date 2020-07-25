---
layout: post
title: Sword to Offer-52 两个链表的第一个公共结点 ❀
---

* 题目描述：  
输入两个链表，找出它们的第一个公共结点。（注意因为传入数据是链表，所以错误测试数据的提示是用其他方式显示的，保证传入数据是正确的）  

## 解题思路：

假设链表1：`a+c`，链表2：`b+c`  
1、若`a==b`，直接能找到第一个相同点；  
2、若`a！=b`，假设`a<b`，`pa`到达终点时，`pb`离终点`b-a`，`pa`到终点后从链表`2`起点开始往后走，
`pb`到达终点时，`pa`已经在链表2走了`b-a`，之后`pb`从链表`1`起点开始走，
当`pb`走了`a`到达交点时，`pa`走了`b-a+a=b`也到达了交点。

同类型的题为[23](http://127.0.0.1:4000/algorithm/2020-04-10-Enterance-of-Circle-in-Linkedlist/)。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-52.png">
</center>


## AC代码：

```java
// The First Common Node of Two LinkedList

public class Solution {
    public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {
        ListNode pNode1 = pHead1;
        ListNode pNode2 = pHead2;
        while (pNode1 != pNode2) {
            pNode1 = (pNode1==null) ? pHead2 : pNode1.next;
            pNode2 = (pNode2==null) ? pHead1 : pNode2.next;
        }
        return pNode1;
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6ab1d9a29e88450685099d45c9e31e46?tpId=13&&tqId=11189&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)