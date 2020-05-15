---
layout: post
title: Test-03 游泳池 ❀
---

* 题目描述：一个自动装置控制给水管和排水管。在开始时，给水管和排水管都是打开状态的，并且游泳池里没有水。在自动装置的作用下，每经过`t1`分钟，给水管的状态都会改变，即从打开状态变为关闭状态或从关闭状态变为打开状态，而同时每经过`t2`分钟，排水管的状态也会改变。  
当给水管打开时，给水管每分钟会向游泳池里注入`m1`升水；当排水管打开时，排水管每分钟会把游泳池里水排走`m2`升；当给水管和排水管同时打开时，游泳池的水量变化为每分钟`(m1-m2)`升。当然泳池的水量不能变为负数，同时泳池也有个最大容量`m`，水量不能超过`m`升。那么经过`t`分钟后，游泳池里有多少升水？

* 输入描述：
> 输入第一行为一个正整数`T`，表示有`T`组数据。  
> 每组数据的为一行包含六个整数，分别表示`m`, `t`, `m1`, `t1`, `m2`, `t2`。  
>   
> 数据范围：  
> 对于所有数据，满足`1<=T<=10`, `1<=m<=100000`, `1<=t<=86400`, `1<=m1,m2<=100`, 
> `1<=t1,t2<=10`。  

* 输出描述：
> 对于每一个数据，输出一行，包括一个整数，为在`t`分钟后游泳池中的水量。

* 输入示例：  
> 5  
> 10 2 1 5 2 5  
> 10 2 10 5 2 5   
> 10 2 3 5 2 5  
> 100 100 3 4 4 3  
> 10000 1000 10 5 5 3  
  
* 输出示例：    
> 0  
> 10  
> 2  
> 3  
> 2495  
 
## 解题思路：

1、判断注水管排水管状态考虑用bool型变量，每次`t%t1==0`时改变注水管状态，排水管同理，注意第一次`t=0`时是不用改变的;  
2、注意，在该分钟内水满和水空的情况需要调整最终水量的值。  

## AC代码：

```java
// Poll Water Injection and Drainage

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int T = scanner.nextInt();
        while (T > 0) {
            int m = scanner.nextInt();
            int t = scanner.nextInt();
            int m1 = scanner.nextInt();
            int t1 = scanner.nextInt();
            int m2 = scanner.nextInt();
            int t2 = scanner.nextInt();
            boolean in = true;
            boolean out = true;
            int res = 0;
            for (int i=0; i<t; i++) {
                if (i!=0 && i%t1==0) {
                    in = !in;
                }
                if (i!=0 && i%t2==0) {
                    out = !out;
                }
                if (in) {
                    res += m1;
                }
                if (out) {
                    res -= m2;
                }
                if (res > m) {
                    res = m;
                }
                if (res < 0) {
                    res = 0;
                }
            }
            System.out.println(res);
            T--;
        }
    }
}
```

## 补充说明：
* 这里是[牛客编码链接](https://www.nowcoder.com/questionTerminal/fc46b8ad830a45698c082ade86904f51?orderByHotValue=1&mutiTagIds=1063&page=1&onlyReference=false)
