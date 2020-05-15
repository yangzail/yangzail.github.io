---
layout: post
title: Test-01 二进制计数 ❀
---

* 题目描述：给定`N`个非负整数，将这`N`个数字按照二进制下`1`的个数分类，二进制下`1`的个数相同的数字属于同一类。求最后一共有几类数字？

* 输入描述：
> 输入的第一行是一个正整数`T（0<T<=10）`，表示样例个数。对于每一个样例，第一行是一个正整数`N（0<N<=100）`，表示有多少个数字。接下来一行是`N`个由空格分隔的非负整数，大小不超过`2^31 – 1`。

* 输出描述：
> 对于每一组样例，输出一个正整数，表示输入的数字一共有几类。

* 输入示例：  
> 1  
> 5  
> 8 3 5 7 2
  
* 输出示例：    
> 3
 
## 解题思路：

1、使用`HashSet`保存每组样例的数据，`HashSet`继承于`Set`，相同的值只能在`Set`中出现一次，所以当出现重复值时，不会被再次保存，将所有输入数据二进制中`1`出现个数的统计添加到`HashSet`中，其结果是每一类（`1`的个数相同为一类）只出现一次，`HashSet`的大小即为总类别数；  
2、使用`n & (n-1)`来判断`n`的二进制表示中`1`出现的次数。

## AC代码：

```java
// How Many One in Binary Number

import java.util.*;

public class Main{
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int T = in.nextInt();  //T个样例
        while (T > 0) {
            int N = in.nextInt();  //该样例含N个元素
            Set<Integer> set = new HashSet<>();
            while (N > 0) {
                int n = in.nextInt();
                set.add(count(n));
                N--;
            }
            System.out.println(set.size());
            T--;
        }
    }
    //  数字n二进制表示中1的个数用该方法求解
    private static int count(int n) {
        int c = 0;
        while (n > 0) {
            n &= n-1;
            c++;
        }
        return c;
    }
}
```

## 补充说明：

* HashSet:  
1、`HashSet` 底层是基于 `HashMap` 实现的；  
2、`HashSet` 除了 `clone()` 、`writeObject()`、`readObject()`是 `HashSet` 单独实现之外，其他方法都是直接调用 `HashMap` 中的方法；  
3、当你把对象加入`HashSet`时，`HashSet`会先计算对象的`hashcode`值来判断对象加入的位置，同时也会与其他加入的对象的`hashcode`值作比较，如果没有相符的`hashcode`，`HashSet`会假设对象没有重复出现。但是如果发现有相同`hashcode`值的对象，这时会调用`equals()`方法来检查`hashcode`相等的对象是否真的相同。  
如果两者相同，`HashSet`就不会让加入操作成功。

* 这里是[牛客编码链接](https://www.nowcoder.com/questionTerminal/d38546d3b0a5416995a84ee9c7128d2b)

* Debug：忘写`T--`，写完循环一定要检查是否改变了循环参数
