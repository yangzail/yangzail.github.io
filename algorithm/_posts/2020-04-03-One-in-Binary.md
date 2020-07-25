---
layout: post
title: Sword to Offer-15 二进制中1的个数 ❀
---

* 题目描述：  
输入一个整数，输出该数`32`位二进制表示中`1`的个数。其中负数用补码表示。


## 解题思路：

数学知识：运算`n = n & (n-1)`相当于将`n`的二进制表示最右边一个`1`变为`0`。


## AC代码：

```java
// One in Binary Number N

public class Solution {
    public int NumberOf1(int n) {
        int count = 0;
        while (n!=0) {
            count++;
            n = n&(n-1);
        }
        return count;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/8ee967e43c2c4ec193b040ea7fbb10b8?tpId=13&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)