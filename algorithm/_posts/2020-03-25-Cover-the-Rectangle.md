---
layout: post
title: Sword to Offer-10.2 矩形覆盖 ❀
---

* 题目描述：我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

* 比如n=3时，2*3的矩形块有3种覆盖方法：  
  
<center>
    <img src="/assets/img/blog/sword-offer-10.2_Example.png">
</center>

## 解题思路：

1、关键在于理解为什么这是斐波那契问题；  
2、当`n=1`时，只有一种摆放方法，当`n=2`时，有两种摆放方法；  
3、当`n=3`时，  
（1）假设第一块竖放，那么接下来是一个`n=2`摆放问题，已知有两种摆放方法；  
（2）假设第一块横放，那么其下面那块区域必须同样横放一个2*n的矩阵，这是第一块横放情况下确定的，所以接下来是一个n=1摆放问题，已知有一种摆放方法；  
（3）第一块横放或者竖放已经包含了第一块所有可能的摆放方式，因而`f(3)=f(2)+f(1)`;  
4、当`n>3`时，情况也如此，`f(n)=f(n-1)+f(n-2)`。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-10.2.png">
</center>


## AC代码：

```java
// Cover a 2*n Rectangle with 2*1 Rectangle

public int RectCover(int target) {
        if (target <= 1) {
            return target;
        }
        int[] method = new int[target+1];
        method[1] = 1;
        method[2] = 2;
        for (int i=3; i<=target; i++) {
            method[i] = method[i-1] + method[i-2];
        }
        return method[target];
    }
```

## 补充说明：

* 注：其实不用保存前面所有n个值，只需要保存前两个即可，具体可见10.3。

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/72a5a919508a4251859fb2cfb987a0e6?tpId=13&tqId=11163&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)