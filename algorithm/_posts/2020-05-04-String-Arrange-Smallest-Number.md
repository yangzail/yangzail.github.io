---
layout: post
title: Sword to Offer-45 把数组排成最小的数 ❀❀
---

* 题目描述：  
输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。  

* 例如输入数组`{3，32，321}`，则打印出这三个数字能排成的最小数字为`321323`。


## 解题思路：

最后的数字需要满足，调换任意一对数字都会让原数字变大（或者不变），可知需要完成的规则为，将数组排列成任何一对数字`A`和`B`（`A`在`B`前面），都满足拼接`A+B`要小于拼接`B+A`，双重循环遍历将数字排成此顺序即可。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-45.png">
</center>


## AC代码：

```java
// Arrange an Array to Smallest Number

import java.util.ArrayList;

public class Solution {
    public String PrintMinNumber(int [] numbers) {
        if (numbers==null || numbers.length==0) {
            return "";
        }
        for (int i=0; i<numbers.length; i++) {
            for (int j=i+1; j<len; j++) {
                //数字之间+""会自动变为字符串，再用Integer.valueOf变回数字
                int numA = Integer.valueOf(numbers[i]+""+numbers[j]);
                int numB = Integer.valueOf(numbers[j]+""+numbers[i]);
                if (numA > numB) {
                    int tmp = numbers[i];
                    numbers[i] = numbers[j];
                    numbers[j] = tmp;
                }
            }
        }
        String numStr = "";
        for (int i=0; i<len; i++) {
            numStr += String.valueOf(numbers[i]);  //返回类型为字符串
        }
        return numStr;
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/8fecd3f8ba334add803bf2a06af1b993?tpId=13&&tqId=11185&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)