---
layout: post
title: Sword to Offer-30 包含min函数的栈 ❀
---

* 题目描述：  
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的`min`函数。  
（时间复杂度应为`O（1）`）


## 解题思路：

1、对于数据栈`dataStack`建立一个最小值栈`minStack`记录其实时最小值；  
2、`dataStack`添加一个新元素时：  
（1）查看`minStack`是否为空，为空表明这是入`dataStack`栈的第一个元素，此时栈内最小值就是新元素，将其`push`到`minStack`；  
（2）不为空的情况下，新元素与与`minStack`顶部元素对比，将其中较小的一个`push`入`minStack`栈。（顶部元素表示在新元素入栈前，`dataStack`栈内的最小值）；  
3、`dataStack`出栈元素时，`minStack`也要出栈一个元素；  
4、读取栈顶元素和读取最小值函数直接返回`dataStack`和`minStack`栈顶值即可。  




## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-30.png">
</center>


## AC代码：

```java
// A Stack With Min Method

import java.util.Stack;

public class Solution {

    private Stack<Integer> dataStack = new Stack<>();
    private Stack<Integer> minStack = new Stack<>();
    
    public void push(int node) {
        dataStack.push(node);
        if (minStack.isEmpty()) {
            minStack.push(node);
        }
        else {
            // 新的最小值要么是原最小值，要么是新添加的值
            if (minStack.peek() < node) {
                minStack.push(minStack.peek());
            }
            else {
                minStack.push(node);
            }
        }
    }
    
    public void pop() {
        dataStack.pop();
        minStack.pop();
    }
    
    public int top() {
        return dataStack.peek();
    }
    
    public int min() {
        return minStack.peek();
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49?tpId=13&&tqId=11173&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)