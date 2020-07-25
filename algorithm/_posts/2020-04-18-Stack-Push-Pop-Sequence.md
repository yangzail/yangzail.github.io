---
layout: post
title: Sword to Offer-31 栈的压入、弹出序列 ❀❀
---

* 题目描述：  
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列`1`,`2`,`3`,`4`,`5`是某栈的压入顺序，序列`4`,`5`,`3`,`2`,`1`是该压栈序列对应的一个弹出序列，但`4`,`3`,`5`,`1`,`2`就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

## 解题思路：

1、外循环：`pushA`中的元素需要依次入栈一次，循环次数为数组长度；  
2、内循环：每放入一个元素进行以此判断，若栈顶元素为`popA`的下一个元素，就将其出栈（隐含条件栈不为空才有栈顶元素），转为匹配`popA`的再下一个元素，若其依旧满足条件，继续上述操作，直至不匹配，此时跳出内循环继续进行`pushA`的元素入栈操作；  
3、最终栈空即匹配，栈不空说明有不可匹配的部分，即不匹配。    


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-31.png">
</center>


## AC代码：

```java
// Whether popA Is pushA's Pop Sequence From A Stack

import java.util.ArrayList;
import java.util.Stack;

public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        if (pushA.length==0 || popA.length==0) {
            return false;
        }
        Stack<Integer> tmpStack = new Stack<Integer>();
        int j = 0;
        for (int i=0; i<pushA.length; i++) {
            tmpStack.push(pushA[i]);
            //将符合popA的序列全部出栈,直至不符合
            while (!tmpStack.isEmpty() && tmpStack.peek()==popA[j]) {
                tmpStack.pop();
                j++;
            }
        }
        //pushA中元素会依次入栈，如果匹配结束还有元素，说明有元素不符合序列，不会出栈
        return tmpStack.isEmpty();
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/d77d11405cc7470d82554cb392585106?tpId=13&&tqId=11174&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)