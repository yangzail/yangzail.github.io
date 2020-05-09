---
layout: post
title: Sword to Offer-11 旋转数组的最小数字 ❀
---

* 题目描述：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。

* 例如数组`{3,4,5,1,2}`为`{1,2,3,4,5}`的一个旋转，该数组的最小值为1。  
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。


## 解题思路：

二分查找(`low<high`则继续查找)：  
1、`mid>high`最小值在`mid+1~high`范围；  
2、`mid<=high`最小值在`low~mid`范围；  
3、注意特殊情况，类似`11101`，当`low=mid=high`只能遍历该部分找解。    

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-11.png">
</center>

## AC代码：

```java
// Finding Minimum Number in Rotate Array

import java.util.ArrayList;

public class Solution {
    public int minNumberInRotateArray(int[] array) {
        if (array.length == 0){
            return 0;
        }
        int low = 0, high = array.length-1;
        while (low < high) {
            int mid = (low + high) / 2;
            if (array[low]==array[mid] && array[mid]==array[high]) {
                return minNum(array, low, high);
            }
            // 注意等于的情况不要乱删数字,不要跳过这个mid
            if (array[mid] <= array[high]) {
                high = mid;
            }
            else {
                low = mid + 1;
            }
        }
        return array[low];
    }
    
    private int minNum(int[] arr, int l, int h) {
        for (int i=l; i<h; i++) {
            if (arr[i] > arr[i+1]) {
                return arr[i+1];
            }
        }
        return arr[l];
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba?tpId=13&tqId=11159&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)