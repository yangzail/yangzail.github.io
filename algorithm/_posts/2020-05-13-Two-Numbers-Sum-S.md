---
layout: post
title: Sword to Offer-57.1 和为 S 的两个数字 ❀
---

* 题目描述：  
输入一个递增排序的数组和一个数字`S`，在数组中查找两个数，使得他们的和正好是`S`，如果有多对数字的和等于`S`，输出两个数的乘积最小的。  
对应每个测试案例，输出两个数，小的先输出。  

## 解题思路：

1、数组为有序的，因此取指针指向头尾，分别向中间靠拢，`left+right=sum`就是积最小的和为`sum`的两个数；  

2、若和大于`sum`，将`right`左移减小和，若小于`sum`将`left`右移增大和，找到了符合条件的两个数或者`right`指针在`left`左边时循环结束。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-57.1.png">
</center>


## AC代码：

```java
// Find Two Number Sum S And Multiply Smallest in Sorted Array

import java.util.ArrayList;



public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
        ArrayList<Integer> res = new ArrayList<>();
        int left = 0, right = array.length - 1;
        while (left < right) {
            if (array[left] + array[right] == sum) {
                res.add(array[left]);
                res.add(array[right]);
                break;
            }
            else if (array[left] + array[right] < sum) {
                left++;
            }
            else {
                right--;
            }
        }
        return res;
    }
}

```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/390da4f7a00f44bea7c2f3d19491311b?tpId=13&&tqId=11195&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)