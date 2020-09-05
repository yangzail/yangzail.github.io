---
layout: post
title: Sword to Offer-10.3 跳台阶 ❀
---

* 题目描述：一只青蛙一次可以跳上`1`级台阶，也可以跳上`2`级。求该青蛙跳上一个`n`级的台阶总共有多少种跳法（先后次序不同算不同的结果）。


## 解题思路：

1、关键在于理解为什么这是斐波那契问题；   
2、当`n=1`时，只有一种跳法，当`n=2`时，有跳两次`1`级和跳一次`2`级两种跳法；   
3、当`n=3`时，    
（1）假设第一次只跳`1`级，那么接下来是一个`n=2`跳跃问题，已知有两种跳法；   
（2）假设第一次跳`2`级，那么接下来是一个`n=1`跳跃问题，已知有一种摆放方法；    
（3）第一次跳1级或者2级已经包含了第一跳所有可能的跳跃方式，因而`f(3)=f(2)+f(1)`;  
4、当`n>3`时，情况也如此，`f(n)=f(n-1)+f(n-2)`;  
5、这次尝试用更少的空间来解决斐波那契问题,不再用一个数组而是只保存当前计算值的前两个值。  

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-10.3.png">
</center>

## AC代码：

```java
// Jump Stairs When Once 1 or 2 Stairs

public class Solution {
    public int JumpFloor(int target) {
        if (target <= 2) {
            return target;
        }
        int prePre = 1;
        int pre = 2;
        int result = 0;
        for (int i=3; i<=target; i++) {
            result = pre + prePre;
            prePre = pre;
            pre = result;
        }
        return result;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/8c82a5b80378478f9484d87d1c5f12a4?tpId=13&tqId=11161&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)