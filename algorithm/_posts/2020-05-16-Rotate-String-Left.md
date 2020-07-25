---
layout: post
title: Sword to Offer-58.2 左旋转字符串 ❀
---

* 题目描述：  
汇编语言中有一种移位指令叫做循环左移`（ROL）`，现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列`S`，请你把其循环左移`K`位后的序列输出。  

* 例如，字符序列`S=”abcXYZdef”`,要求输出循环左移`3`位后的结果，即`“XYZdefabc”`。是不是很简单？OK，搞定它！

## 解题思路：

思路1：用辅助数组储存前`n`个值，其余字符左移完成后，将辅助数组的值传给最后`n`个字符。  

思路2：先分别翻转前后两部分，再翻转整个字符串。  


## 解法一、辅助数组

### AC代码：  

```java
// Rotate String Left

public class Solution {
    public String LeftRotateString(String str,int n) {
        if (str==null || str=="" || str.length()==0) {
            return "";
        }
        char[] chs = str.toCharArray();
        int len = chs.length;
        char[] tmp = new char[n];
        for (int i=0; i<n ;i++) {
            tmp[i] = chs[i];
        }
        for (int i=0; i<len-n; i++) {
            chs[i] = chs[i+n];
        }
        for (int i=0; i<n; i++) {
            chs[len-n+i] = tmp[i];
        }
        String s = String.valueOf(chs);
        return s;
    }
}

```

## 解法二、翻转字符串

### 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-58.2.png">
</center>

### AC代码：  

```java
// Rotate String Left

public class Solution {
    public String LeftRotateString(String str,int n) {
        int len = str.length();
        if (str == null || len < n) {
            return "";
        }
        char[] chs = str.toCharArray();
        reverse(chs, 0, n-1);
        reverse(chs, n, len-1);
        reverse(chs, 0, len-1);
        String rotateStr = String.valueOf(chs);
        return rotateStr;
    }
     
    private void reverse(char[] chs, int begin, int end) {
        while (begin < end) {
            char tmp = chs[begin];
            chs[begin] = chs[end];
            chs[end] = tmp;
            begin++;
            end--;
        }
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/12d959b108cb42b1ab72cef4d36af5ec?tpId=13&&tqId=11196&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)