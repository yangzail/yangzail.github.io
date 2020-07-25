---
layout: post
title: Sword to Offer-53 数字在排序数组中出现的次数 ❀
---

* 题目描述：  
统计一个数字在排序数组中出现的次数。 

## 解题思路：

比遍历更简单的方法是递归找中点：  
1、返回条件为子数组`low>high`，即子数组不存在元素了，返回值取`-1`，因为该方法返回的是`int`类型数组下标，如果返回`0`的话，意为找到了`k`在下标为`0`的位置而不是不存在`k`；  
2、否则查找其中值是否等于要找的元素`k`，等于则返回其下标`mid`；  
3、不等于则继续递归查找左右子序列的中值，具体为中值大于`k`则对左子数组递归，小于`k`则对右子序列递归；  
最后根据返回的等于`k`的元素的下标，分别向左右做两次遍历，找总共有多少个值等于`k`。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-53.png">
</center>


## AC代码：

```java
// The First Common Node of Two LinkedList

public class Solution {
    public int GetNumberOfK(int [] array , int k) {
        if (array==null || array.length==0) {
            return 0;
        }
        int count = 0;
        int low = 0;
        int high = array.length - 1;
        int index = findMid(array, low, high, k);
        if (index == -1) {
            return count;
        }
        int indexTmp = index;
        while (indexTmp>=0 && array[indexTmp]==k) {
            indexTmp--;
            count++;
        }
        while (index<=array.length-1 && array[index]==k) {
            index++;
            count++;
        }
        count--;  // 处于index处的k被判断了两遍
        return count;
    }
    
    private int findMid(int[] array, int low, int high, int k) {
        int mid = (low + high) / 2;
        if (low > high) {
            return -1;
        }
        if (array[mid] == k) {
            return mid;
        }
        if (array[mid] > k) {
            return findMid(array, low, mid - 1, k);
        }
        else {
            return findMid(array, mid + 1, high, k);
        }
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/70610bf967994b22bb1c26f9ae901fa2?tpId=13&&tqId=11190&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)