---
layout: post
title: Sword to Offer-21 调整数组顺序使奇数位于偶数前面 ❀
---

* 题目描述：  
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。


## 解题思路：

1、遍历一遍数组，分别记录下奇数偶数的个数；  
2、以奇数个数为划分点，是用两个指针分别指向排列后的奇数和偶数的第一个位置；  
3、遍历一遍数组的副本，遍历时将每个值分别放到原数组奇偶指针处，指针后移一位。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-21.png">
</center>


## AC代码：

```java
// Adjust for Even Numbers Before Odds When Order Unchanged

public class Solution {
    public void reOrderArray(int [] array) {
        int arrLen = array.length;
        int numEven = 0;
        
        for (int i=0; i<arrLen; i++) {
            if (array[i]%2 != 0) {
                numEven++;
            }
        }
        int[] arrTmp = array.clone();
        int indexEven = 0; //奇数从0位置开始放
        int indexOdd = numEven; //偶数从numEven位置开始放
        //因为要返回原数组，所以先copy到arrTmp，遍历时放入原数组
        for (int i=0; i<arrLen; i++) {
            if (arrTmp[i]%2 != 0) {
                array[indexEven] = arrTmp[i];
                indexEven++;
            }
            else {
                array[indexOdd] = arrTmp[i];
                indexOdd++;
            }
        }
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/beb5aa231adc45b2a5dcc5b62c93f593?tpId=13&&tqId=11166&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)