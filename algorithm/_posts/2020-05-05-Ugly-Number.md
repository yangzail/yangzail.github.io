---
layout: post
title: Sword to Offer-49 丑数 ❀❀
---

* 题目描述：  
把只包含质因子`2`、`3`和`5`的数称作丑数（Ugly Number）。例如`6`、`8`都是丑数，但`14`不是，因为它包含质因子7。 习惯上我们把`1`当做是第一个丑数。求按从小到大的顺序的第`N`个丑数。


## 解题思路：

第一个丑数设为`1`，直接添加到丑数`ArrayList`中，接下来以`2`,`3`,`5`为因子乘以确定的偶数因子`1`，得到三个值中最小的一个添加到丑数`ArrayList`中，且被选中的那个因子再下一次比较中，应该乘以数组下一个数，其他因子的乘法不变。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-49.png">
</center>


## AC代码：

```java
// Arrange an Array to Smallest Number

import java.util.List;
import java.util.ArrayList;
import java.lang.Math;

public class Solution {
    public int GetUglyNumber_Solution(int index) {
        if (index <= 1) {
            return index;
        }
        List<Integer> uglyNum = new ArrayList<>();
        uglyNum.add(1);
        int index2 = 0;
        int index3 = 0;
        int index5 = 0;
        while (uglyNum.size() < index) {
            int num2 = uglyNum.get(index2) * 2;
            int num3 = uglyNum.get(index3) * 3;
            int num5 = uglyNum.get(index5) * 5;
            int minNum = Math.min(num2, Math.min(num3, num5));
            uglyNum.add(minNum);
            if (minNum == num2) {
                index2++;
            }
            if (minNum == num3) {
                index3++;
            }
            if(minNum == num5) {
                index5++;
            }
        }
        return uglyNum.get(uglyNum.size()-1);
    }
}
```


## 补充说明： 

* 注意：`Math.max`方法只能有两个参数，所以三数比较时需要用两遍。  
   
* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6aa9e04fc3794f68acf8778237ba065b?tpId=13&&tqId=11186&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)