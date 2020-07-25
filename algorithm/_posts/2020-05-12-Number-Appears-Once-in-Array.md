---
layout: post
title: Sword to Offer-56 数组中只出现一次的数字 ❀❀
---

* 题目描述：  
一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

## 解题思路：

可用`HashMap`进行求解，参考[41.2]（）和[50]（）。  

此处介绍另一种方法，用异或特性求解：  
1、异或特性，`num^0 = num`; `num^num = 0`  
2、首先将所有数异或一下，所有成对的数异或起来最终结果为`0`，可知最终结果即为所求这两个数`X`和`Y`的异或；  
3、由于这两个数肯定不同，得出至少有一位不同，也就是说是最终结果中一定存在`1`；  
4、取出这个`1`，寻找的两个数在这个位置肯定不同，找到这个位置，将数组按该位的值分为两组，`X`和`Y`会分别在两组中；  
5、与此同时，相同的数字该位一定相同，也会在同一组。结果形如`[abcbcaX]``[dYfdefe]`；  
6、此时分别对两组数的全部数字进行异或，结果即为`X`和`Y`。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-56.png">
</center>


## AC代码：

```java
// Find Two Number Appear Once When Others Appear Twice in Array

public class Solution {
    public void FindNumsAppearOnce(int [] array,int num1[] , int num2[]) {
        if (array == null || array.length <= 1) {
            num1[0] = num2[0] = 0;
            return;
        }
        int len = array.length;
        int xorRes = 0;  //保存X^Y结果
        for (int i=0; i<len; i++) {
            xorRes ^= array[i];
        }
        int positionOf1 = 0;  //保存X^Y从右到左第一个1的下标位置
        while (positionOf1 < len) {
            if ((xorRes & (1<<positionOf1)) != 0) {
                break;
            }
            positionOf1++;
        }
        num1[0] = 0;
        num2[0] = 0;
        // 分组异或求X和Y
        for (int i=0; i<len; i++) {
            if ((array[i] & (1<<positionOf1)) == 0) {
                num1[0] ^= array[i];
            }
            else {
                num2[0] ^= array[i];
            }
        }
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/e02fdb54d7524710a7d664d082bb7811?tpId=13&&tqId=11193&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)