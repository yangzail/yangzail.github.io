---
layout: post
title: Sword to Offer-14 剪绳子 ❀❀
---

* 题目描述：给你一根长度为`n`的绳子，请把绳子剪成整数长的`m`段（`m`、`n`都是整数，`n>1`并且`m>1`），每段绳子的长度记为`k[0]`,`k[1]`,...,`k[m]`。请问`k[0] x k[1] x...x k[m]`可能的最大乘积是多少？例如，当绳子的长度是`8`时，我们把它剪成长度分别为`2`、`3`、`3`的三段，此时得到的最大乘积是`18`。


## 解题思路：

动态规划  
1、用一个动态规划数组来储存长度为`i`时，可得的最大绳子切割乘积，假设`j`在`1~i-1`之间，用于切割长度为`i`的绳子，那么该绳子的最大乘积就是`两部分的最大乘积之积`的最大值;  
2、注意绳长`target<=3`时，作为一根完整的绳子，由于必须被切割，其最大切割乘积为`1`,`1`,`2`,但作为更长绳子的一部分可以得到`1`,`2`,`3`所以要单独设置:  
(1) 前三种情况题设条件得到的最优解为`1`,`1`,`2`;  
(2) 但当它们作为绳长的一部分时，最优解是不剪切得到的`1`,`2`,`3`;  
3、`target>3`，比如`target=4`的时候，必须剪切情况下可以得到`2*2=4`，不剪情况下得到的也是`4`，`target=5`的时候，必须剪切得到`2*3=6`，不剪切得到`5`；也就是说，从`target=4`开始往后，可以看作剪切一定能得到比不剪切更优解;  


  

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-14.png">
</center>

## AC代码：

```java
// The Range in Which the Robot Can Move

public class Solution {
    public int cutRope(int target) {
        if (target <= 2) {
            return 1;
        }
        if (target == 3) {
            return 2;
        }
        int[] dp = new int[target+1];
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        for (int i=4; i<=target; i++) {
            for (int j=1; j<i; j++) {
                dp[i] = Math.max(dp[i], dp[j]*dp[i-j]);
            }
        }
        return dp[target];
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/57d85990ba5b440ab888fc72b0751bf8?tpId=13&tqId=33257&tPage=4&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)