---
layout: post
title: Sword to Offer-66 构建乘积数组  ❀❀
---

* 题目描述：  
给定一个数组`A[0,1,...,n-1]`,请构建一个数组`B[0,1,...,n-1]`,其中`B`中的元素`B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]`。不能使用除法。  

* 注意：规定`B[0] = A[1] * A[2] * ... * A[n-1]`，`B[n-1] = A[0] * A[1] * ... * A[n-2]`。

## 解题思路：

思路1：暴力双重循环，求`B[i]`时除了下标为`i`的那个数，其他数直接连乘。  

思路2：动态规划：
1、`leftMulti`记录左边下标为`[0~i]`数的积，表示`A`数组前`i+1`个数的积，`rightMulti`记录右边下标为`[i~n-1]`的积，表示`A`数组后`n-i`个数的积；  
2、所求的`B[i] = leftMulti[i-1] * rightMulti[i+1]`，即为左边部分的连乘*右边部分的连乘；  
3、特殊值，`B`第一个值为`rightMulti[1]`，最后一个值为`left[n-2]`。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-66.png">
</center>


## AC代码：

方法1、暴力双重循环:  

```java
// Multiply All Numbers in Array Except Position i

import java.util.ArrayList;

public class Solution {
    public int[] multiply(int[] A) {
        int[] B = new int[A.length];
        if (A==null || A.length==0) {
            return B;
        }
        for (int i=0; i<A.length; i++) {
            B[i] = 1;
            for (int j=0; j<A.length; j++) {
                if (i != j){
                    B[i] *= A[j];
                }
            }
        }
        return B;
    }
}
```

方法2、动态规划，空间换时间：

```java
import java.util.ArrayList;

public class Solution {
    public int[] multiply(int[] A) {
        int n = A.length;
        int[] B = new int[n];
        if (A==null || n==0) {
            return B;
        }
        int[] leftMulti = new int[n];
        int[] rightMulti = new int[n];
        leftMulti[0] = A[0];
        for (int i=1; i<n; i++) {
           leftMulti[i] = leftMulti[i-1] * A[i]; 
        }
        rightMulti[n-1] = A[n-1];
        for (int i = n-2; i>=0; i--) {
            rightMulti[i] = rightMulti[i+1] * A[i];
        }
        B[0] = rightMulti[1];
        B[n-1] = leftMulti[n-2];
        for (int i=1; i<n-1; i++) {
            B[i] = leftMulti[i-1] * rightMulti[i+1];
        }
        return B;
    }
}
```

## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/94a4d381a68b47b7a8bed86f2975db46?tpId=13&&tqId=11204&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)