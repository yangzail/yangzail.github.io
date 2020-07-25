---
layout: post
title: Sword to Offer-59 滑动窗口的最大值 ❀❀
---

* 题目描述：  
给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组`{2,3,4,2,6,2,5,1}`及滑动窗口的大小`3`，那么一共存在`6`个滑动窗口，他们的最大值分别为`{4,4,6,6,6,5}`；   
针对数组`{2,3,4,2,6,2,5,1}`的滑动窗口有以下`6`个： `{[2,3,4],2,6,2,5,1}`， `{2,[3,4,2],6,2,5,1}`， `{2,3,[4,2,6],2,5,1}`， `{2,3,4,[2,6,2],5,1}`， `{2,3,4,2,[6,2,5],1}`， `{2,3,4,2,6,[2,5,1]}`。

## 解题思路：

思路1：两次循环对每个窗口求最大值并储存。  

思路2：采用双向队列进行处理，队头总保持为当前滑动窗口最大值的下标，具体如下：  
  
1、每新进一个元素，从队尾开始遍历队列，看该下标对应的数组元素是否小于自身，小于自身的元素全部从队尾删除，最后将自己插到队尾；  
2、插入到队尾后判断当前的队头，也就是将要添加到列表的当前滑动窗口最大元素是否已经脱离滑动窗口，其有可能为本次滑动将要删除的数的下标，如果是此情况，将需要其删除，即从队头弹出该元素；  
3、查看当前是否已经形成滑动窗口，如果只处理到前面`size-1`个元素，是无法形成长为`size`的滑动窗口的，如果已经形成，将队头保存下来，它就是当前最大值的下标，否则继续处理下一个数。  
(重点在于出队入队的方向)  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-59.png">
</center>


## AC代码：

1、双重循环：

```java
// Maximun Number of All Sliding Windows in Array

import java.util.ArrayList;

public class Solution {
    public ArrayList<Integer> maxInWindows(int [] num, int size)
    {
        ArrayList<Integer> maxOfWindow = new ArrayList<>();
        if (size>num.length || size<1) {
            return maxOfWindow;
        }
        for (int i=0; i<=num.length-size; i++) {
            int max = num[i];
            for (int j=i; j<i+size; j++) {
                if (num[j] > max) {
                    max = num[j];
                }
            }
            maxOfWindow.add(max);
        }
        return maxOfWindow;
    }
}

```

2、借助双向队列：  

```java
// Maximun Number of All Sliding Windows in Array

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Deque;

public class Solution {
    public ArrayList<Integer> maxInWindows(int [] num, int size) {
        if (num == null || num.length == 0 || size <= 0 || num.length < size) {
            return new ArrayList<Integer>();
        }
        ArrayList<Integer> result = new ArrayList<>();
        // 双端队列，队头记录每个窗口的最大值下标
        Deque<Integer> deque = new LinkedList<>();
        for (int i = 0; i < num.length; i++) {
            // 弹出队尾不如当前值大的元素
            while (!deque.isEmpty() && num[i]>num[deque.peekLast()]) {
                deque.pollLast();
            }
            deque.addLast(i);
            // 判断队首元素是否超出窗口范围
            if (deque.peekFirst() == i-size) {
                deque.pollFirst();
            }
            // 判断是否已经形成窗口
            if (i >= size-1) {
                result.add(num[deque.peekFirst()]);
            }
        }
        return result;
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/1624bc35a45c42c0bc17d17fa0cba788?tpId=13&&tqId=11217&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)