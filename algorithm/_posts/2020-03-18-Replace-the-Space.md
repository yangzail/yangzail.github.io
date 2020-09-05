---
layout: post
title: Sword to Offer-05 替换空格 ❀
---

* 题目描述：请实现一个函数，将一个字符串中的每个空格替换成`“%20”`。  

* 例如，当字符串为`We Are Happy`，则经过替换之后的字符串为`We%20Are%20Happy`。

## 解题思路：

1、注意到替换后字符串长度更长，需要扩展字符串长度，如果从前往后处理，会覆盖原信息；  
2、遍历一遍`string`，出现一个空格，字符串长度`+2`；  
3、用两个指针`j`，`k`分别指向扩展前后的`string`末尾，从后往前遍历`string`；   
4、`j`非空格，复制`j`到`k`，`j`和`k`一起左移一次；`j`为空格，`k`依次添加`02%`左移三次，`j`左移一次。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-05.png">
</center>


## AC代码：

```java
// Replace the space in a string with %20

public class Solution {
    public String replaceSpace(StringBuffer str) {
        //str length before
        int len_before = str.length() - 1;  
        // find a ' ', string append two spaces
        for (int i=len_before; i>=0; i--) {
            if (str.charAt(i) == ' ') {
                str.append("  ");
            }
        }
        
        // string has a new length longer than before
        int len_after = str.length() - 1;

        int j = len_before;   
        int k = len_after;    
        // traversal the string back to front
        for(; k>0; k--, j--) {
            char c = str.charAt(j);
            // if j is not a ' ',copy it to k
            // else k should add '0','2','%' in order
            if (c != ' ') {
                str.setCharAt(k, c);
            }
            else {
                str.setCharAt(k, '0');
                k--;
                str.setCharAt(k, '2');
                k--;
                str.setCharAt(k, '%');
            }
        }
        // return should be a String class not StringBuffer
        return str.toString();
    }
}
```
## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/4060ac7e3e404ad1a894ef3e17650423?tpId=13&tqId=11155&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)