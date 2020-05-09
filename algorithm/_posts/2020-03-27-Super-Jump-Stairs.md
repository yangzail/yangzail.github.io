---
layout: post
title: Sword to Offer-10.4 变态跳台阶 ❀
---

* 题目描述：一只青蛙一次可以跳上1级台阶，也可以跳上2级...它也可以跳上 n 级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。


## 解题思路：

1、区别于上一个跳台阶问题（普通斐波那契问题）;     
2、第一次可以跳`1~n`级;    ，    
（1）假设第一次只跳1级，那么接下来是一个`f(n-1)`跳跃子问题；     
（2）假设第一次跳k级，那么接下来是一个`f(n-k)`跳跃子问题；  
（3）假设第一次跳n-1级，那么接下来是一个`f(1)`跳跃子问题，此时`f(1)=1`，因为第一次跳了n-1级，第二次只能跳一级，只有这种固定的可能；  
（4）最后是第一次就跳了n级，此时为`f(0)=1`，一次跳完；   
3、简化计算公式  
（1）`f(n)=f(n-1)+f(n-2)+…+f(1)+f(0)`    
（2）`f(n-1)=f(n-2)+f(n-3)+…+f(1)+f(0)`  
（3）两式相减可得`f(n)=2*f(n-1)`    
4、计算`f(n)`实际上只需要保存下`f(n-1)`的值，需要保留的值只有一个。
  

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-10.4.png">
</center>

## AC代码：

```java
// Jump Stairs When Once 1~n Stairs

public int JumpFloorII(int target) {
        if (target <=2) {
            return target;
        }
        int pre = 2;
        int result = 0;
        for (int i=3; i<=target; i++) {
            result = 2 * pre;
            pre = result;
        }
        return result;
    }
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/22243d016f6b47f2a6928b4313c85387?tpId=13&tqId=11162&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)