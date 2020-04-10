---
layout: post
title: Sword to Offer-04 二维数组中的查找 ❤
---

* 在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

* 例如，对于矩阵
```js
[
    [1, 3, 4, 7, 18,22]
    [2, 6, 9, 10,20,27]
    [5, 8, 12,17,23,36]
    [15,19,21,30,40,41]
]
```
输入17，输出true；  
输入25，输出false。

## 解题思路：

1、注意到此矩阵左上角为最小值，右下角为最大值，从中间值开始查找效率最高；  
2、假定从右上角开始寻找，target大于选中值坐标下移，target小于选中值坐标左移；  
3、遍历一次矩阵，每次比较后，向着更接近target的方向移动；  
4、特殊情况是，遍历完成也没有找到。

## 主流程图：

<center>
    <img alt="An image" src="/assets/img/blog/sword-offer-04.png">
</center>


## AC代码：

```java
// Search a target in a partially ordered 2D matrix

public boolean Find(int target, int [][] array) {
        // get the number of rows and columns of array
        int rows = array.length;
        int columns = array[0].length;
        // if array is null return false
        if (array == null || rows==0 || columns==0)
            return false;
        // begin with a medium number
        int i = 0;
        int j = columns-1;
        // traverse until found or boundary.
        // if target bigger,turn down,i++;
        // if target smaller,turn left,j--;
        while ((array[i][j]!=target) && (i<rows-1) && (j>0)) {
            if (target > array[i][j]){
                i++;
            }
            else {
                j--;
            }
        }
        
        // the cycle quit with target found or boundary touched 
        if (array[i][j] == target) {
            return true;
        }
        else {
            return false;
        }
    }
```
## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e?tpId=13&tqId=11154&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)