---
layout: post
title: Sword to Offer-09 用两个栈实现队列 ❀
---

* 题目描述：用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。 

## 解题思路：

1、保证每个元素两次入栈+两次出栈即可；   
2、一个栈用于push，另一个栈用于pop,保证每个元素都走完stack1入栈，出栈，stack2入栈，出栈这四个流程，完成两次逆序；  
3、push简单入栈stack1，pop若stack2有元素直接出栈，stack2栈空时，先将stack1所有元素转移过来再出栈；  
4、特殊情况，转移过后stack2也还是空，抛出异常`Queue is empty`。


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

* 注意：将stack1元素transfer到stack2的时间点。先进stack2的元素是先push的元素，pop优先级一定高于stack1现存的元素，故stack2为空之前pop操作是轮不到stack1元素出栈的，stack2为空时才考虑transfer过来。

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=13&tqId=11158&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)