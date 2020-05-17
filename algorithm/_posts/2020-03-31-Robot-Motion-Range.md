---
layout: post
title: Sword to Offer-13 机器人的运动范围 ❀❀
---

* 题目描述：地上有一个`m`行和`n`列的方格。一个机器人从坐标`(0, 0)`的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于`k`的格子。 例如，当`k`为`18`时，机器人能够进入方格`（35, 37）`，因为`3 + 5 + 3 + 7 = 18`。但是，它不能进入方格`（35, 38）`，因为`3 + 5 + 3 + 8 = 19`。请问该机器人能够达到多少个格子？


## 解题思路：

1、对任意一个点，不需要反复搜寻的固定起点的回溯法，只要不出矩阵范围且满足条件，就将该点标记为已走过，继续走不符合条件也不用改变原本被选中点的状态；  
2、以`(0, 0)`为起点，向周围搜寻，判断的点不满足条件返回`0`，满足则向周围继续搜寻，返回周围能找到的个数`+ 1`（本身）。
  

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-13.png">
</center>

## AC代码：

```java
// The Range in Which the Robot Can Move

public class Solution {
    public int movingCount(int threshold, int rows, int cols) {
        // set a matrix to sign status
        boolean[][] status = new boolean[rows][cols];
        int i =0, j = 0;  //initial position
        return backTracking(status, rows, cols, i, j, threshold);
    }
    private int backTracking(boolean status[][], int rows, int cols,
                                                    int i, int j, int threshold) {
        // out of boundary or has been selected or bigger than threshold
        if (i<0 || i>=rows || j<0 || j>=cols || status[i][j] || sumBit(i,j)>threshold)
            return 0;
        // if not return means find a position satisfied,set the status to true
        status[i][j] = true;
        return backTracking(status, rows, cols, i-1, j, threshold) +
               backTracking(status, rows, cols, i+1, j, threshold) +
               backTracking(status, rows, cols, i, j-1, threshold) +
               backTracking(status, rows, cols ,i, j+1, threshold) + 1;
    }
     // calculate the sum of every bit of i and j
     private int sumBit(int i, int j) {
         int sum = 0;
         while (i != 0) {
             sum += i % 10;
             i = i / 10;
         }
         while (j != 0) {
             sum += j % 10;
             j = j / 10;
         }
         return sum;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6e5207314b5241fb83f2329e89fdecc8?tpId=13&tqId=11219&tPage=4&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)