---
layout: post
title: Sword to Offer-41.1 数据流中的中位数 ❀
---

* 题目描述：  
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用`Insert()`方法读取数据流，使用`GetMedian()`方法获取当前读取数据的中位数。


## 解题思路：

`int`和`Integer`区别：  
`int`是一种基本数据类型，一般用于一些简单的加减乘除运算；  
`Integer`为`int`的封装类，还提供了很多面向对象的方法，如最常用的`valueOf`。


## AC代码：

```java
// Find Median in Data Stream

import java.util.ArrayList;
import java.util.Collections;

public class Solution {
    ArrayList<Integer> list = new ArrayList<>();
    public void Insert(Integer num) {
        list.add(num);
        Collections.sort(list);
    }

    public Double GetMedian() {
        int n = list.size();
        if (n % 2 == 0) {
            //注意数据下标，还有注意除以2.0才能自动转换为double相除，否则会舍位
            return Double.valueOf((list.get(n/2) + list.get(n/2-1)) / 2.0);
        }
        else {
            return Double.valueOf(list.get(n/2));
        }
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&&tqId=11182&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)