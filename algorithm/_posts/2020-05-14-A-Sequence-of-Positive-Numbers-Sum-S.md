---
layout: post
title: Sword to Offer-57.2 和为S的连续正数序列  ❀❀
---

* 题目描述：  
小明很喜欢数学,有一天他在做数学作业时,要求计算出`9~16`的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为`100`(至少包括两个数)。没多久,他就得到另一组连续正数和为`100`的序列:`18`,`19`,`20`,`21`,`22`。现在把问题交给你,你能不能也很快的找出所有和为`S`的连续正数序列?   
Good Luck!

* 输出描述：  
输出所有和为`S`的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序。

## 解题思路：
变长滑动窗口问题：  
1、初始`begin`和`end`为`1`和`2`，循环条件为`begin<=sum/2`；  
2、当前窗口内数字总和`<sum`时，`end++`，当前窗口内数字总和`>sum`时，`begin++`；  
3、恰好`=sum`时找到了一个满足条件的序列，此时新建一个临时`ArrayList`将窗口内的值添加到其中，让将该`ArrayList`添加到需要返回的`ArrayList`列表内；  
4、找到满足的序列后，`begin++`，`end++`继续搜索；
5、注意指针移动和修改当前`sum`值的先后顺序，`begin`指针应先修改`sum`再移动，`end`指针应先移动再修改`sum`值。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-57.2.png">
</center>


## AC代码：

```java
// Find All Consecutive Sequences of Positive Number Sum S

import java.util.ArrayList;

public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer>> seqs = new ArrayList<>();
        int begin = 1, end = 2;
        int curSum = 3;
        while (begin <= sum/2) {
            if (curSum > sum) {
                curSum -= begin;
                begin++;
            }
            else if (curSum < sum) {
                end++;
                curSum += end;
            }
            else {
                ArrayList<Integer> seqSingle = new ArrayList<>();
                for (int i=begin; i<=end; i++) {
                    seqSingle.add(i);
                }
                seqs.add(seqSingle);
                curSum -= begin;
                begin++;
                end++;
                curSum += end;
            }
        }
        return seqs;
    }
}

```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/c451a3fd84b64cb19485dad758a55ebe?tpId=13&&tqId=11194&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)