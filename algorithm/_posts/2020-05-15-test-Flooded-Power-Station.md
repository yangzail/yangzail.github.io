---
layout: post
title: Test-04 水平线 ❀❀？
---

* 当洪水淹没基站时，基站只能停止发电，同时被迫断开与相邻基站的链接。在洪水到来时，计算出发电集群被洪水淹没后被拆分成了多少个集群。  
给定一维数组`a`，长度为`n`，表示了`n`个基站的位置高度信息。数组的第`i`个元素`a[i]`表示第i个基站的海拔高度是`a[i]`,而下标相邻的基站才相邻并且建立链接，即`x`号基站与`x-1`号基站、`x+1`号基站相邻。特别的，`1`号基站仅与`2`号相邻，而`n`号基站仅与`n-1`号基站相邻。当一场海拔高度为`y`的洪水到来时，海拔高度小于等于`y`的基站都会被认为需要停止发电，同时断开与相邻基站的链接。

* 输入描述：
> 每个输入数据包含一个测试点。  
>   
> 第一行为一个正整数`n`，表示发电基站的个数 (`0 < n <= 200000`)  
>   
> 接下来一行有`n`个空格隔开的数字，表示`n`个基站的海拔高度，第`i`个数字`a[i]`  
> 即为第`i`个基站的海拔高度，对于任意的`i`(`1<=i<=n`),有(`0 <= a[i] < 2^31-1`)  
>   
> 接下来一行有一个正整数`q`(`0 < q <= 200000`)，表示接下来有`q`场洪水  
>   
> 接下来一行有`q`个整数，第`j`个整数`y[j]`表示第`j`场洪水的海拔为`y[j]`,  
> 对于任意的`j`(`1<=j<=n`),有(`-2^31 < y[j] < 2^31-1`)  

* 输出描述：
> 输出`q`行，每行一个整数，第`j`行的整数`ans`表示在第`j`场洪水中，发电基站会被分割成`ans`个集群。
> 标准答案保证最后一个整数后也有换行。

* 输入示例：  
> 10  
> 6 12 20 14 15 15 7 19 18 13   
> 6  
> 15 23 19 1 17 24    
  
* 输出示例：    
> 2  
> 0  
> 1  
> 1  
> 2  
> 0  
 
## 解题思路：

1、对于每一个洪水水位线，遍历一遍所有水电站，每当有一个水电站高度大于洪水水位，判定集群`+1`,该集群延续到下一个被淹没的水电站为止；    
2、该思路估计没错，但是超时了。

## AC（40%）代码：

```java
// Flooded Power Station 

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] a = new int[n];
        for (int i=0; i<n; i++) {
            a[i] = scanner.nextInt();
        }
        int q = scanner.nextInt();
        int[] y = new int[q];
        for (int i=0; i<q; i++) {
            y[i] = scanner.nextInt();
        }
        for (int j=0; j<q; j++) {
            int count = 0;
            int i = 0;
            while (i < n) {
                if (a[i] > y[j]) {
                    count++;
                    i++;
                    while (i<n && a[i]>y[j]) {
                        i++;
                    }
                }
                i++;
            }
            System.out.println(count);
        }
    }
}
```

## 补充说明：
* 这里是[牛客编码链接](https://www.nowcoder.com/questionTerminal/5e029c555f194ffa8e6c9cbc2adbefc0)
