---
layout: post
title: Test-02 幸运N串 ❀
---

* 题目描述：一个全部由大写字母组成的字符串，允许改变最多`2`个大写字母（也允许不改变或者只改变`1`个大写字母），使得字符串中所包含的最长的连续的`N`串的长度最长。

* 输入描述：
> 输入的第一行是一个正整数`T``（0 < T <= 20）`，表示有`T`组测试数据。对于每一个测试数据包含一行大写字符串`S`（`0 < |S| <= 50000`，`|S|`表示字符串长度）。
> 数据范围：
`20%`的数据中，字符串长度不超过`100`；  
`70%`的数据中，字符串长度不超过`1000`；  
`100%`的数据中，字符串长度不超过`50000`。

* 输出描述：
> 对于每一组测试样例，输出一个整数，表示操作后包含的最长的连续N串的长度。

* 输入示例：  
> 3  
> NNTN  
> NNNNGGNNNN  
> NGNNNNGNNNNNNNNSNNNN
  
* 输出示例：    
> 4  
> 10  
> 18  
 
## 解题思路：

1、将字符串中的非`N`字符视为分隔符号，将字符串看作由相隔的几段`N`串组成;  
2、使用动态规划方法，在遍历字符串的过程，`m1`初始值为上一段`N`串字符串个数（上一个包括非`N`字符），`m2`初始值为上两段`N`串字符串个数（包括上两个非`N`字符）；  
3、在遍历第三段`N`串的过程中，`count`用于记录第三段`N`串当前已遍历的`N`个数，`m1`用于记录`前一个串长度`+`当前串已遍历N个数`，`m2`用于记录`前两个N串长度`+`当前串已遍历N个数`；  
4、`m2`每次达到最大值的时候，是刚碰见第三个非`N`字符的时候，此时`m2`为三串子`N`串（包括两个非`N`字符）长度之和，即为所求幸运`N`串长度。

## AC代码：

```java
// Lucky String N

import java.util.*;

public class Main{
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int T = in.nextInt();  //T个字符串
        while (T > 0) {
            String str = in.next();
            int count = 0;  //保存当前N串N的个数之和
            int n1 = 0; 
            int n2 = 0;  //保存前1,2段N串N的个数+当前串已遍历N个数之和
            int res = 0;  //最大N串N个数
            for(int i=0; i<str.length(); i++) {
                if (str.charAt(i) == 'N') {
                    count++;
                    n1++;
                    n2++;
                }
                else {
                    n2 = n1 + 1;  //更新m2初始值为上两段长度（包括两个非N字符）
                    n1 = count + 1;  //更新m1初始值为上一段长度（包括非N字符）
                    count = 0;   //更新count初值记录新N串长度
                }
                // 遍历过程中modify2能达到的最大值即为所求的res
                res = Math.max(res, n2);
            }
            System.out.println(res);
            T--;
        }
    }
}
```

## 补充说明：
* 这里是[牛客编码链接](https://www.nowcoder.com/questionTerminal/3d08b635346d4610b01c6256bc07c394?orderByHotValue=1&mutiTagIds=1063&page=1&onlyReference=false)


