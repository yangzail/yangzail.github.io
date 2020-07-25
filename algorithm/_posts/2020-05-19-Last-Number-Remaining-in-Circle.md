---
layout: post
title: Sword to Offer-62 圆圈中最后剩下的数 ❀❀
---

* 题目描述：  
每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:  
首先,让小朋友们围成一个大圈。然后,他随机指定一个数`m`,让编号为`0`的小朋友开始报数。每次喊到`m-1`的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续`0...m-1`报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？  
(注：小朋友的编号是从`0`到`n-1`)  

如果没有小朋友，请返回`-1`。

## 解题思路：

两种方法思路一致：  
使用数组或者链表来遍历数字`0~n-1`，当步长走到`m`时，删除该元素，重置步长为`0`，当遍历到结尾下标为`n`时，将其改回`0`模拟圆圈。当数组或链表剩下最后一个元素时，输出即可。  

用数组会麻烦一点，注意各个变量的意义即可。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-62.png">
</center>


## AC代码：

1、用数组来模拟游戏：

```java
// Last Number in Circle 

public class Solution {
    public int LastRemaining_Solution(int n, int m) {
        if (n<1 || m<1) {
            return -1;
        }
        boolean[] isOut = new boolean[n]; //指示是否被删除
        int i = -1;  //在数组中的位置
        int step = 0;  //实际走过的长度
        int remain = n;  //剩余元素个数
        while (remain > 0) {
            i++; //数组中的位置每次循环都+1
            // 末尾元素的下个元素是第一个元素
            if (i == n) {
                i = 0;
            }
            // 如果位置为i的元素被删除了，看下一个元素，step不用++
            if (isOut[i]) {
                continue;
            }
            step++;  //走过的长度只有isOut==false才+1
            // 走过的步长等于m时，将此处元素标记为out，步长重置为0，remain元素-1,
            if (step == m) {
                isOut[i] = true;
                step = 0;
                remain--;
            }
        }
        return i;  // i指向最后一个被out的元素
    }
}
```

2、用链表来模拟游戏：  

```java
// Last Number in Circle

import java.util.ArrayList;
import java.util.List;

public class Solution {
   public static int LastRemaining_Solution(int n, int m) {
        if (n < 1 || m < 1)
            return -1;
        List<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            list.add(i);
        }
        int index = 0;
        while (list.size() > 1) {
            for (int j = 1; j < m; j++) {
                if (index == list.size() - 1)
                    index = 0;
                else
                    index++;
            }
            list.remove(index);
            if (index == list.size())
                index = 0;
        }
        return list.get(0);
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/f78a359491e64a50bce2d89cff857eb6?tpId=13&&tqId=11199&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)