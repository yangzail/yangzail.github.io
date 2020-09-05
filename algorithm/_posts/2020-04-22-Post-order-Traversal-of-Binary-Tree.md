---
layout: post
title: Sword to Offer-33 二叉搜索树的后序遍历序列 ❀❀
---

* 题目描述：  
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出`Yes`,否则输出`No`。假设输入的数组的任意两个数字都互不相同。  

## 解题思路：

根据二叉搜索树特性，相当于判断序列是不是按照小大中的顺序来排列，左子树结点全部小于根结点全部小于右子树结点。判断时，先确定`root`的值。再根据此值划分前面的序列为左右子树的结点值，再对左右子树进行递归判定：  
1、如果子序列的长度`<=1`，可直接判定该子序列满足条件；  
2、以序列中第一个大于`root`的值作为分界点，右边序列如果出现小于`root`值，可判定子序列为不符合规律。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-33.png">
</center>


## AC代码：

```java
// Whether popA Is pushA's Pop Sequence From A Stack

public class Solution {
    public boolean VerifySquenceOfBST(int [] sequence) {
        if (sequence == null || sequence.length == 0) {
            return false;
        }
        return verify(sequence, 0, sequence.length-1);
    }
    
    private boolean verify(int[] sequence, int begin, int end) {
        //已确定单点是大于或小于根的，所以只有单点的时候已经可以判断true
        if (end-begin <= 1) {
            return true;
        }
        int root = sequence[end];
        int cutPoint = begin;
        while (cutPoint<end && sequence[cutPoint]<=root) {
            cutPoint++;
        }
        for (int i=cutPoint; i<end; i++) {
            if (sequence[i] < root) {
                return false;
            }
        }
        return verify(sequence, begin, cutPoint-1) && verify(sequence, cutPoint, end-1);
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/a861533d45854474ac791d90e447bafd?tpId=13&&tqId=11176&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)