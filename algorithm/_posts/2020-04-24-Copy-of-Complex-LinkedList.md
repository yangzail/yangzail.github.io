---
layout: post
title: Sword to Offer-35 复杂链表的复制 ❀❀❀
---

* 题目描述：  
输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针`random`指向一个随机节点），请对此链表进行深拷贝，并返回拷贝后的头结点。  
（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空） 

## 解题思路：

遍历三遍：  
1、将原链表每个结点复制一份，复制的新结点插入到原结点后面，此时`random`域依旧为空；  
2、使用`pNode`和`copy`两个指针一起遍历链表，`pNode`总是指向原结点，`copy`总是指向复制的新结点，将`copy`结点的`random`域指向原结点`random`域指向的结点的复制;  
3、使用前后两个指针，通过改变结点的`next`域拆分两个链表。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-35.png">
</center>


## AC代码：

```java
// Deep Copy A LinkedList with Random Area

/*
public class RandomListNode {
    int label;
    RandomListNode next = null;
    RandomListNode random = null;

    RandomListNode(int label) {
        this.label = label;
    }
}
*/

public class Solution {
    public RandomListNode Clone(RandomListNode pHead)
    {
        if (pHead == null) {
            return null;
        }
        RandomListNode pNode = pHead;
        //添加复制结点
        while (pNode != null) {
            RandomListNode copyNode = new RandomListNode(pNode.label);
            copyNode.next = pNode.next;
            pNode.next = copyNode;
            pNode = copyNode.next;
        }
        //给复制结点的random赋值
        pNode = pHead;
        while (pNode != null) {
            RandomListNode copy = pNode.next;
            //考虑原来结点random为空的情况
            if (pNode.random != null) {
                copy.random = pNode.random.next;
            }
            pNode = copy.next;
        }
        //拆分成两个链表
        pNode = pHead;
        RandomListNode copyHead = pHead.next; //新链表的头结点
        while (pNode.next != null) {
            RandomListNode pNext = pNode.next;
            pNode.next = pNext.next;
            pNode = pNext;
        }
        return copyHead;
    }
}
```

## 补充说明：

* 浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存;但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象。  

* 注意考虑原链表的`random`域就为空的情况。  

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/b736e784e3e34731af99065031301bca?tpId=13&&tqId=11177&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)