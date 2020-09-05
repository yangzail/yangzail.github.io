---
layout: post
title: Sword to Offer-19 正则表达式匹配 ❀❀❀
---

* 题目描述：  
请实现一个函数用来匹配包括`'.'`和`'*'`的正则表达式。模式中的字符`'.'`表示任意一个字符，而`'*'`表示它前面的字符可以出现任意次（包含`0`次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。  
例如，字符串`"aaa"`与模式`"a.a"`和`"ab*ac*a"`匹配，但是与`"aa.a"`和`"ab*a"`均不匹配。


## 解题思路：

用一个判定函数调用自身来分治此问题：  
1、返回`true`条件：两个字符串同时匹配到末尾；  
2、若`pattern`到尾时`string`还有字符未匹配，直接返回`false`；  
3、其他情况：  
（运行到此处说明`pattern`还未匹配完，或者`pattern`和`string`均未匹配完）  
（1）若`pattern`不是最后一位且下一位为`‘*’`  
此情况下若`string`未匹配完且当前位匹配成功，要么是`pattern`当前位可匹配多次，对应`string`的指针`+1`，要么是`pattern`当前位出现`0`次，此时`pattern`的指针`+2`；  
其他情况，即当前不匹配，或者`string`已匹配完，此时`sIndex`指向非法值，也可视为当前不匹配的特殊情况，此时能匹配的情况只能抱希望于`*`之前的字符出现`0`次，故`pattern`指针`+2`；  
（2）若`string`未到尾且当前匹配成功（相同字符或者`pattern`为`‘.’`），将`string`和`pattern`的指针同时`+1`即可。  


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-19.png">
</center>

## AC代码：

```java
// Regular Expression Matching Judge

public class Solution {
    public boolean match(char[] str, char[] pattern)
    {
        if (str == null || pattern == null) {
            return false;
        }
        int sIndex = 0;
        int pIndex = 0;
        return match(str, sIndex, pattern, pIndex);
    }
    
    private boolean match(char[] str, int sIndex, char[] pattern, int pIndex) {
        //两个指针同时到尾匹配成功
        if (sIndex==str.length && pIndex==pattern.length) {
            return true;
        }
        //pattern先到尾，匹配失败
        if (sIndex!=str.length && pIndex==pattern.length) {
            return false;
        }
        //匹配未结束且pattern下一个字符为*
        if (pIndex+1<pattern.length && pattern[pIndex+1]=='*') {
            //当前字符匹配下一个为*,该字符出现多次对应sIndex+1,出现0次对应pIndex+2
            if (sIndex!=str.length && (str[sIndex]==pattern[pIndex] || pattern[pIndex]=='.')) {
                return match(str, sIndex+1, pattern, pIndex) || match(str, sIndex, pattern, pIndex+2);
            }
            //当前不匹配下一个为*，pattern跳过两个字符
            else {
                return match(str, sIndex, pattern, pIndex+2);
            }
        }
        //如果未匹配结束，且pattern当前字符为'.'或匹配成功，直接匹配两个串的下一个字符
        else if (sIndex!=str.length && (str[sIndex]==pattern[pIndex] || pattern[pIndex]=='.')) {
                return match(str, sIndex+1, pattern, pIndex+1);
            }
        //匹配未结束，当前匹配失败，下一个字符也不为*，直接return false
        else {
            return false;
        }
    }
}
```

## 补充说明：

* 注意：  
1、关键点在于是处理与`‘*’`相关的情况，下一位为`‘*’`，可能是`‘*’`前的字符在`string`中出现多次，`sIndex+1`,或者不出现`pIndex+2`,若当前位不匹配或者`string`的当前位已经是`null`的特殊情况，只能选择`pIndex+2`；  
2、实际上`Java`数组下标越界不是`null`而是`out of bound eror`。

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/45327ae22b7b413ea21df13ee7d6429c?tpId=13&&tqId=11205&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)