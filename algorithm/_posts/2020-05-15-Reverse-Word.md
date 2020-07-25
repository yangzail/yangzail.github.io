---
layout: post
title: Sword to Offer-58.1 翻转单词顺序列 ❀
---

* 题目描述：  

牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。  
例如，`“student. a am I”`。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是`“I am a student.”`。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

## 解题思路：

思路1、用`split`方法划分字符串，再倒序输出字符串数组，注意数组中最后一个字符串后不需接`“ ”`。  
思路2、先翻转每个句子，再翻转每个单词。


## 解法一、倒序输出字符串数组

### AC代码：

```java
// Reverse the Word

public class Solution {
    public String ReverseSentence(String str) {
        if (str==null || str=="" || str.length()==0) {
            return "";
        }
        String[] strs = str.split(" ");
        int len = strs.length;
        if (len == 0) {
            return str;
        }
        String reverseWord = "";
        for (int i=len-1; i>=0; i--) {
            reverseWord += strs[i];
            if (i == 0) {
                break;
            }
            reverseWord += " ";
        }
        return reverseWord;
    }
}
```

## 解法二、翻转字符串

### 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-58.1.png">
</center>

### AC代码：

```java
// Reverse the Word

public class Solution {
    public String ReverseSentence(String str) {
        int len = str.length();
        char[] chs = str.toCharArray();
        reverse(chs, 0, len-1);  // 翻转整个句子
        int begin = 0;
        for (int i=0; i<len; i++) {
            if (chs[i] == ' ') {
                reverse(chs, begin , i-1);
                begin = i + 1;
            }
        }
        // 注意处理最后一个字符串
        reverse(chs, begin, len-1);
        String strReverse = String.valueOf(chs);
        return strReverse;
    }
     
    private void reverse(char[] chs, int begin, int end) {
        while (begin < end) {
            char tmpCh = chs[begin];
            chs[begin] = chs[end];
            chs[end] = tmpCh;
            begin++;
            end--;
        }
    }
}
```

## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/3194a4f4cf814f63919d0790578d51f3?tpId=13&&tqId=11197&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)