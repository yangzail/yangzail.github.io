---
layout: post
title: Sword to Offer-42 连续子数组的最大和 ❀
---

* 题目描述：  
HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:  
在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？  
例如:`{6,-3,-2,7,-15,1,2,2}`,连续子向量的最大和为`8`(从第`0`个开始,到第`3`个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是`1`)


## 解题思路：

动态规划问题：  
设`F(i)`为以`array`从头到下标为`i`的子序列和的最大值，  
那么有`F(i) = max(F(i-1)+array[i], array[i])`;  
`F(i)`中的最大值即为所求最大子序列和。  

思路1、用一个动态规划数组来保存前`i+1`个元素组成的子序列和的最大值，该数组中的最大值即为所求最大序列和。  
思路2、简化版，只需要保存上一个子序列和的最大值。  


## 解法一、动态规划

### 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-42.png">
</center>


### AC代码：

```java
// Find the Max Sum Sequence in Array

public class Solution {
    public int FindGreatestSumOfSubArray(int[] array) {
        if (array==null || array.length==0) {
            return 0;
        }
        int n = array.length;
        int[] sumMax = new int[n];
        sumMax[0] = array[0];  //序列至少含一个元素
        int max = array[0];
        for (int i=1; i<n ; i++) {
            //sumMax[i]表示以i为尾的子序列最大和
            sumMax[i] = Math.max(sumMax[i-1]+array[i], array[i]);
            //max记录sumMax数组中的最大值
            max = Math.max(sumMax[i], max);
        }
        return max;
    }
}
```
注：由于下标问题，遍历从`1`开始，此时要设置`sumMax`和`max`的初值，都是设置为`array[0]`，因为当子序列只有第一个元素时，`sumMax`和`max`都等于`array[0]`。  
  

## 解法二：只存最大值

### AC代码：

```java
// Find the Max Sum Sequence in Array

public class Solution {
    public int FindGreatestSumOfSubArray(int[] array) {
        if (array==null || array.length==0) {
            return 0;
        }
        int sumMax = 0;
        int max = Integer.MIN_VALUE;  
        for (int i=0; i<array.length; i++) {
            //sumMax[i]表示到以i为尾的子序列最大和
            sumMax = Math.max(array[i], sumMax+array[i]);
            //max记录所有序列的最大和（不用以i为尾）
            max = Math.max(max, sumMax);
        }
        return max;
    }
}
```
注：这次用一个数而不是数组来记录上一个子序列的最大和，遍历可从`0`开始，此时上一个序列为空，记录的`sumMax`值为`0`，而`max`初值应取最小整型数值，这样可以保证遍历到第一个数时，子序列的`max`一定为第一个元素。 （可以看到当此程序运行到`i=1`时，恰好对应上一版本的初值。）  

## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/459bd355da1549fa8a49e350bf3df484?tpId=13&&tqId=11183&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)