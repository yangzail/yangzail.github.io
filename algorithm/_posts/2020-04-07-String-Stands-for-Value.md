---
layout: post
title: Sword to Offer-20 表示数值的字符串 ❀❀
---

* 题目描述：  
请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。  
例如，字符串`"+100"`,`"5e2"`,`"-123"`,`"3.1416"`和`"-1E-16"`都表示数值。 但是`"12e"`,`"1a3.14"`,`"1.2.3"`,`"+-5"`和`"12e+4.3"`都不是。


## 解题思路：

1、正则表达式规则如下：
`[]`字符集合，指此处可出现集合中存在的任意字符；  
`()`分组；  
`？`重复`0-1`次；  
`+`重复`1-n`次；  
`*`重复`0-n`次；  
`.`任意字符；  
`\\.`转义后的.；  
`\\d`数字  
2、构成数字的规则：  
正负号，小数部分`（.d）`，指数部分`（e+3）`，指数部分的符号`（+-）`都只能不出现或出现一次；  
整数部分数字出现`0-n`次，可以不出现，小数和指数部分数字出现`1-n`次，至少要有一次。


## AC代码：

```java
// String Stands for a Value or Not

public class Solution {
    public boolean isNumeric(char[] str) {
        if (str == null || str.length == 0) {
            return false;
        }
        return new String(str).matches("[+-]?[\\d]*(\\.[\\d]+)?([eE][+-]?[0-9]+)?");
    }
}
```

## 补充说明：

* 注意：数学问题，先分区域，再根据规则从外到里写。  

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6f8c901d091949a5837e24bb82a731f2?tpId=13&&tqId=11206&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)