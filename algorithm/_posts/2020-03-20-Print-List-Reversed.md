---
layout: post
title: Sword to Offer-06 从尾到头打印链表 ❀
---

* 题目描述：输入一个链表，按链表从尾到头的顺序返回一个`ArrayList`。  


## 解题思路：

* 倒序输出链表问题  
思路1、头插法，创建头结点，遍历链表元素，依次插入为头结点的下一个结点。  
思路2、使用栈，遍历链表元素，依次入栈，遍历完成后依次出栈。

## 解法一：头插法

### 问题图解：

<center>
    <img alt="An image" src="/assets/img/blog/sword-offer-06_1.png">
</center>

### AC代码：

```java
// Head inserting 

public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        // construct a head node
        ListNode head = new ListNode(-1);
        // node's next is head's next and head's next is this node
        // record the latter node,otherwise cannot find it after operation
        while (listNode != null) {
            ListNode latter = listNode.next;
            listNode.next = head.next;
            head.next = listNode;
            listNode = latter;
        }
        
        // move it to an arraylist
        ArrayList<Integer> array = new ArrayList<>();
        // get the first node of linklist
        head = head.next;
        while (head != null) {
            array.add(head.val);
            head = head.next;
        }
        return array;
    }
}
```

## 解法二：使用栈

### 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-06_2.png">
</center>

### AC代码：

```java
// Use Stack 

public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        // define a Stack to push listNodes
        Stack<Integer> stackTmp =  new Stack<>();
        while (listNode != null) {
            stackTmp.push(listNode.val);
            listNode = listNode.next;
        }
        // define a ArrayList to get stack pops
        ArrayList<Integer> ret = new ArrayList<>();
        while (!stackTmp.isEmpty()) {
            ret.add(stackTmp.pop());
        }
        return ret;
    }
```

## 补充说明：

* 使用栈时记得`import java.util.Stack`  
* 这里是[牛客编码链接](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035?tpId=13&tqId=11156&tPage=1&rp=4&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)