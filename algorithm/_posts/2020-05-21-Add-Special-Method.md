---
layout: post
title: Sword to Offer-65 不用加减乘除做加法 ❀❀
---

* 题目描述：  
写一个函数，求两个整数之和，要求在函数体内不得使用`+`、`-`、`*`、`/`四则运算符号。

## 解题思路：

加法的一种神奇算法:  
1、两个数异或，结果为两个数各位相加不考虑进位的结果；  
2、两个数相与，结果为发生进位的位；  
3、相与的结果左移一位加上异或的结果，即为两数相加结果；  
4、这个相加又没办法用`+`号，所以递归求解，直到表示进位的相与结果为`0`，此时输出相异或结果，即可得到最终的相加结果。  


## AC代码：

```java
// Special Way to Calculate Add

public class Solution {
    public int Add(int num1, int num2) {
        if (num2 == 0) {
            return num1;
        }
        else {
            int sum = num1 ^ num2;
            int carray = (num1 & num2) << 1;
            return Add(sum, carray);
        }
    }
}
```


## 补充说明： 

* 注意：  

  思考过能否在`if`语句后面添加判定若满足`num1==0`，输出`num2<<1`，即添加如下两行：
```java
        else if (num1 == 0) {
            return num2 << 1;
        }
```
实际上不可行，原因在于，如果第一次输入的时候`num1`就等于`0`，那么两者的和就直接输出`num2`就好，如输入`0`，`-4`，应该输出`-4`，而添加了以上判定后会输出错误答案`-8`。此时的`num2`不是表示该进位的位，而是表示原本的数字。如果要加判定是否是第一次运行`Add`方法的参数又太麻烦了，所以还是直接以`num2==0`为递归退出判定条件的好。


* 这里是[牛客编码链接](https://www.nowcoder.com/practice/59ac416b4b944300b617d4f7f111b215?tpId=13&&tqId=11201&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)