---
layout: post
title: Sword to Offer-12 矩阵中的路径 ❀
---

* 题目描述：请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 

* 例如  
<img src="/assets/img/blog/sword-offer-12_example.png">
矩阵中包含一条字符串`"bcced"`的路径，但是矩阵中不包含`"abcb"`路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。


## 解题思路：

回溯法  
1、


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