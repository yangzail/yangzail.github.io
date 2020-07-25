---
layout: post
title: Sword to Offer-29 顺时针打印矩阵 ❀
---

* 题目描述：  
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。  

* 例如：如果输入如下`4 X 4`矩阵： `1` `2` `3` `4` `5` `6` `7` `8` `9` `10` `11` `12` `13` `14` `15` `16`, 则依次打印出数字`1`,`2`,`3`,`4`,`8`,`12`,`16`,`15`,`14`,`13`,`9`,`5`,`6`,`7`,`11`,`10`。  

<center>
    <img src="/assets/img/blog/sword-offer-29.1.png">
</center>


## 解题思路：

1、用四个指针记录下目前还未遍历的最大最小行数列数；  
未被遍历的最小行数大于最大行数，或者最小列数大于最大列数的时候，终止循环；  
（即，循环条件为同时满足两组`min<=max`）  

2、每一次循环转一个环形读取数据，需注意边界的取值：  
（1）向右`→`的遍历可从`min`遍历到`max`，向下`↓`的遍历可从`min+1`遍历到`max`，向左`←`的遍历可以从`max-1`遍历到`min`，向上`↑`的遍历可以从`max-1`遍历到`min+1`；  
（2）每完成一次环状遍历后，缩小范围，`min`值`+1`，`max`值`-1`。  



## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-29.2.png">
</center>


## AC代码：

```java
// Print Maxtrix's Elements Clockwise

import java.util.ArrayList;

public class Solution {
    public ArrayList<Integer> printMatrix(int [][] matrix) {
        //用于返回的ArrayList
        ArrayList<Integer> ret = new ArrayList<>();
        int rowMin = 0, rowMax = matrix.length - 1;
        int colMin = 0, colMax = matrix[0].length - 1;
        while (rowMin<=rowMax && colMin<=colMax) {
            for (int i=colMin; i<=colMax; i++) {
                ret.add(matrix[rowMin][i]);
            }
            for (int i=rowMin+1; i<=rowMax; i++) {
                ret.add(matrix[i][colMax]);
            }
            if (rowMin != rowMax) {
                for (int i=colMax-1; i>=colMin; i--) {
                    ret.add(matrix[rowMax][i]);
                }
            }
            if (colMin != colMax) {
                for (int i=rowMax-1; i>rowMin; i--) {
                    ret.add(matrix[i][colMin]);
                }
            }
            rowMin++;
            rowMax--;
            colMin++;
            colMax--;
        }
        return ret;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/9b4c81a02cd34f76be2659fa0d54342a?tpId=13&&tqId=11172&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)