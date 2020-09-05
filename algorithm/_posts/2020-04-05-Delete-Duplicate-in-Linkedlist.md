---
layout: post
title: Sword to Offer-18.2 删除链表中重复的结点 ❀❀
---

* 题目描述：  
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表`1->2->3->3->4->4->5` 处理后为 `1->2->5`。


## 解题思路：

用前后两个指针`preNode`和`pNode`遍历链表；  
1、一般情况下同时移动两个`Node`；  
2、每当`pNode`和其`next`结点的值相同，向后移动`pNode`直至不相等，此时`pNode`指向的是最后一个相同值；  
3、将`preNode`（上一个应当保留的结点）指向`pNode`的下一个结点（继续扫描开始的结点），就可以删除`pNode`走过而`preNode`未走过的所有相同的值；  
同时为了继续遍历要移动`pNode`指向其下一个结点。   


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-18.2.png">
</center>

## AC代码：

```java
// Delete Duplicate Number in Linklist

public class Solution {
    public ListNode deleteDuplication(ListNode pHead)
    {
        if (pHead==null || pHead.next==null) {
            return pHead;
        }
        // add a new head node before pHead to return
        // cause pHead may be same as pHead.next
        ListNode headNode = new ListNode(0);
        headNode.next = pHead;
        // preNode is the last node of new linklist
        ListNode preNode = headNode;
        // pNode travese the linklist
        ListNode pNode = pHead;
        while (pNode!=null) {
            // if pNode has next and its val equals pNode.next's val
            // drop all of them, move pNode util the end or a new number
            if (pNode.next!=null && pNode.val==pNode.next.val) {
                while (pNode.next!=null && pNode.val==pNode.next.val) {
                    pNode = pNode.next;
                }
                // pNode is the last number ths time we drop
                preNode.next = pNode.next;
                pNode = pNode.next;
            }
            else {
                // pNode's val not equal pNode.next's val, move together
                preNode = preNode.next;
                pNode = pNode.next;
            }
        }
        // headNode never move and point the headNode we create
        // its next is the first node of new linklist
        return headNode.next;
    }
}
```

## 补充说明：

* 注意：  
1、本题要求返回链表头指针，而`preNode`和`pNode`都是移动的，需要记录下头指针位置，可新建一个结点指向`pHead`，其`next`用于返回；  
2、看清本题要求将重复元素全部删除，`1->2->3->3->4->4->5` 处理后为 `1->2->5`，出现了重复的元素包括其本身全部删除。  

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/fc533c45b73a41b0b44ccba763f866ef?tpId=13&&tqId=11209&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)