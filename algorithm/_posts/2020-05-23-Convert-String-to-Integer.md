---
layout: post
title: Sword to Offer-67 把字符串转换成整数 ❀
---

* 题目描述：  

将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为`0`或者字符串不是一个合法的数值则返回`0`。

* 输入描述：  
输入一个字符串,包括数字字母符号,可以为空。  

* 输出描述：  
如果是合法的数值表达则返回该数字，否则返回0。  

* 输入示例：  
`+2147483647`  
`1a33`  

* 输出示例：  
`2147483647`  
`0`  


## 解题思路：

遍历一遍字符串：  
1、判断首字符是否为符号，如果是，在取得该数正负号情况后，用`continue`截断此次循环直接进入下一次；  
2、判断首字符的时候，使用一个标志位记录是否为负数，若首字符为`‘-’`可将标志位置为`true`，表示该数为负数；  
3、若首字符不是正负号，或进入了第二个字符发处理，接下来判断字符是否超出了`‘0’~‘9’`的范围，超出范围直接`return 0`，看到不是数字；  
4、若以上都满足，将当前数字记为 =上一位字符对应的数字 `*10` + 本位字符对应的数字；  
5、遍历完成后，看符号标志位是否为`true`，如果是的话将最终的数字`*(-1)`；  
6、最后要看最终数字是否符合`Integer`的范围，若未超出范围则转换成`int`类型输出，否则也是失败，只能`return 0`。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-67.png">
</center>


## AC代码：

```java
// Judge String Can Be Converted to A Integer Or Not

public class Solution {
    public int StrToInt(String str) {
        if (str == null || str.length() == 0) {
            return 0;
        }
        char[] chs = str.toCharArray();
        boolean isNegative = false;
        long num = 0;
        for (int i=0; i<str.length(); i++) {
            if ((i==0) && (chs[i]=='+' || chs[i]=='-')) {
                if (chs[0] == '-') {
                    isNegative = true;
                }
                continue;
            }
            if (chs[i] < '0' || chs[i] > '9') {
                return 0;
            }
            num = num * 10 + (chs[i] - '0');
        }
        if (isNegative) {
            num *= -1;
        }
        if (num > Integer.MAX_VALUE || num < Integer.MIN_VALUE) {
            return 0;
        }
        else {
            return (int)num;
        }
    }
}

```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/1277c681251b4372bdef344468e4f26e?tpId=13&&tqId=11202&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)