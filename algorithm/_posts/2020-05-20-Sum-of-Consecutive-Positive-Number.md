---
layout: post
title: Sword to Offer-64 求 1+2+3+...+n ❀❀
---

* 题目描述：  
求`1+2+3+...+n`，要求不能使用乘除法、`for`、`while`、`if`、`else`、`switch`、`case`等关键字及条件判断语句`（A?B:C）`。

## 解题思路：

循环的递归写法：  
1、`n！=0`就会继续递归，否则就可出递归，输出`sum`值了;  
2、`sum`是必定`>0`的, 加判断只是为了让表达式正确，形如`boolean&&boolean`;  
3、定义`boolean`类型的变量`tmp`也是为了语句合理，通过编译，并无任何实际意义。


## AC代码：

```java
// Special Way of Writing Loop

public class Solution {
    public int Sum_Solution(int n) {
        int sum = n;
        boolean tmp = (n>0) && ((sum += Sum_Solution(n-1))>0);
        return sum;
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/7a0da8fc483247ff8800059e12d7caf1?tpId=13&&tqId=11200&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)