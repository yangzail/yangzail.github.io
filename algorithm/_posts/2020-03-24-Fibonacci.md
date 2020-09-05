---
layout: post
title: Sword to Offer-10.1 斐波那契数列 ❀
---

* 题目描述：要求输入一个整数`n`，请你输出斐波那契数列的第`n`项。（从`0`开始，第`0`项为`0`）

* 解释：斐波那契数列
<img src="/assets/img/blog/sword-offer-10.1_Fibonacci.png">
 
## 解题思路：

1、如果按照函数表达式递归计算，每次计算`f(n)`都要重新递归计算`f(n-1)`和`f(n-2)`的值；  
2、考虑空间换时间，已计算完成的`f(n)`储存到一个数组里，下次计算就只要调用数组相应下标的值即可;  
3、注意：要计算`f(n)`需要`f(0)~f(n-1)`一共n个值，所以数组长度为`n+1`；  
4、注意：`n=0`情况要单独返回，因为要设定初值`f(0)`和`f(1)`，输入`n`为`0`时，new的数组长度为`1`，此时如果设定初值`f(1)`会报错哦。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-10.1.png">
</center>


## AC代码：

```java
// Fibonacci Sequence

public class Solution {
    public int Fibonacci(int n) {
        if (n == 0) {
            return n;
        }
        int[] fib = new int[n+1];
        fib[0] = 0;
        fib[1] = 1;
        for (int i=2; i<=n; i++) {
            fib[i] = fib[i-1] + fib[i-2];
        }
        return fib[n];
    }
}
```

## 补充说明：

* 注：这题和`10.2`，`10.3`类型相似，计算`f(n)`其实不用保存前面所有`n`个值，只需要保存前两个即可，具体可见`10.3`。

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/c6c7742f5ba7442aada113136ddea0c3?tpId=13&tqId=11160&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)