---
layout: post
title: Sword to Offer-39 数组中出现次数超过一半的数字 ❀
---

* 题目描述：  
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为`9`的数组{`1`,`2`,`3`,`2`,`2`,`2`,`5`,`4`,`2`}。由于数字`2`在数组中出现了`5`次，超过数组长度的一半，因此输出`2`。如果不存在则输出`0`。


## 解题思路：

寻找主元素问题：  
1、遍历数组，假设第一个元素为主元素，将其保存，将`count`设为`1`，之后遇见该元素`count++`；否则`count--`，`count==0`时，切换该位置元素为新的主元素，`count`重新置为`1`；  
2、遍历完成后，有可能是主元素的值已被保存，再遍历一次数组记录下其真实出现次数，大于数组长度的一半即为主元素，否则不存在。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-39.png">
</center>


## AC代码：

```java
// Find the Number Occurs More Than Half Length in Array

public class Solution {
    public int MoreThanHalfNum_Solution(int [] array) {
        if (array==null || array.length<=0) {
            return 0;
        }
        
        int majorElement = array[0];
        int count = 1;
        for (int i=1; i<array.length; i++) {
            if (array[i] == majorElement) {
                count++;
            }
            else {
                count--;
            }
            if (count == 0) {
                majorElement = array[i];
                count = 1;
            }
        }
        
        int numOfMajor = 0;
        for (int val : array) {
            if (val == majorElement) {
                numOfMajor++;
            }
        }
        return numOfMajor>array.length/2 ? majorElement : 0;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=13&&tqId=11181&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)