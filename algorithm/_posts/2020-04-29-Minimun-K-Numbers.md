---
layout: post
title: Sword to Offer-40 最小的 K 个数 ❀
---

* 题目描述：  
输入`n`个整数，找出其中最小的`K`个数。例如输入`4`,`5`,`1`,`6`,`2`,`7`,`3`,`8`这`8`个数字，则最小的`4`个数字是`1`,`2`,`3`,`4`。


## 解题思路：

冒泡排序，外循环设为`k`次即可得到最小的`k`个值，相邻的两个值比较，将最小的值往右冒泡至无序部分的最后一个位置，每次外循环将冒泡上去的那个数添加到用于返回的链表中。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-40.png">
</center>


## AC代码：

```java
// Find the k Minimum Numbers in Array （Bubble Sort）

import java.util.ArrayList;

public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> res = new ArrayList<>();
        if (input == null || k<=0 || k>input.length) {
            return res;
        }
        for (int i=0; i<k; i++) {
            for (int j=0; j<input.length-i-1; j++) {
                if (input[j] < input[j+1]) {
                    int tmp = input[j];
                    input[j] = input[j+1];
                    input[j+1] = tmp;
                }
            }
            res.add(input[input.length-i-1]);
        }
        return res;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&&tqId=11182&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)