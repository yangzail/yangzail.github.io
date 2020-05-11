---
layout: post
title: Sword to Offer-09 用两个栈实现队列 ❀
---

* 题目描述：用两个栈来实现一个队列，完成队列的`Push`和`Pop`操作。 队列中的元素为`int`类型。 

## 解题思路：

1、保证每个元素两次入栈, 两次出栈即可；   
2、一个栈用于`push`，另一个栈用于`pop`,保证每个元素都走完`stack1`入栈，出栈，`stack2`入栈，出栈这四个流程，完成两次逆序；  
3、`push`简单入栈`stack1`，`pop`若`stack2`有元素直接出栈，`stack2`栈空时，先将`stack1`所有元素转移过来再出栈；  
4、特殊情况，转移过后`stack2`也还是空，抛出异常`Queue is empty`。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-09.png">
</center>


## AC代码：

```java
// Using Two Stacks Implements the Function of a Queue

// stack1 is the in stack
public void push(int node) {
    stack1.push(node);
}
    
// stack 2 is the out stack
public int pop() throws Exception{
    // if stack2 is empty,see stack1 and transfer to stack2
    if (stack2.isEmpty()) {
        while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
        }
    }

    // after transfer,pop from stack2 or throw exception
    if (stack2.isEmpty()) {
        throw new Exception("queue is empty!");
    }
        return stack2.pop();
}
```

## 补充说明：

* 注意：将`stack1`元素transfer到`stack2`的时间点。先进`stack2`的元素是先`push`的元素，`pop`优先级一定高于`stack1`现存的元素，故`stack2`为空之前`pop`操作是轮不到`stack1`元素出栈的，`stack2`为空时才考虑`transfer`过来。

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=13&tqId=11158&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)