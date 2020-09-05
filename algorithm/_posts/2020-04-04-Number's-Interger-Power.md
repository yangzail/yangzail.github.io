---
layout: post
title: Sword to Offer-16 数值的整数次方 ❀
---

* 题目描述：  
给定一个`double`类型的浮点数`base`和`int`类型的整数`exponent`。求`base`的`exponent`次方。
保证`base`和`exponent`不同时为`0`

## 解题思路：

主要考察数学上的分类情况  
1、底数为`0`：`0`的`0`次方无意义，`0`的非`0`次方为`0`;  
2、底数非`0`：先按正数进行连乘计算次方，若为负数的次方，则需要求倒数。  

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-16.png">
</center>

## AC代码：

```java
// Number's Integer Power

public class Solution {
    public double Power(double base, int exponent) {
        if (base==0) {
            if (exponent==0) {
                return -1;  //0的0次方无意义
            }
            else {
                return 0;  //0的非0次方等于0
            }
        }
        double res = 1;  //res为最终结果，初始值为1
        boolean minus = false;  //指示次方是否为负数
        if (exponent<0) {
            minus = true;
            exponent = -exponent;
        }
        while (exponent>0) {
            res = res * base;
            exponent--;
        }
        return minus ? 1/res : res;
  }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/1a834e5e3e1a4b7ba251417554e07c00?tpId=13&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)