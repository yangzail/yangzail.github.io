---
layout: post
title: Sword to Offer-50 第一个只出现一次的字符位置 ❀
---

* 题目描述：  
在一个字符串(`0<=字符串长度<=10000`，全部由字母组成) 中找到第一个只出现一次的字符，并返回它的位置，如果没有则返回 `-1`（从`0`开始计数，需要区分大小写）。

## 解题思路：  

思路1：可用与[41.2](http://127.0.0.1:4000/algorithm/2020-05-01-First-No-Repeated-Character-in-Stream/)一样的方法，利用`HashMap`求解。  

思路2：直接遍历的方法，使用一个数组来记录每个元素出现的次数。数组下标为字符，会自动转换为该字符的`ASCII`码，数组值为该字符出现次数。第一次遍历记录，第二次遍历找到第一个数组值为`1`的位置，输出即可。 两次遍历的实际下标顺序都是字符串中每个字符依次的`ASCII`码。  


## 解法一、使用HashMap

### AC代码：

```java
// Get the Position of Character Appears Once in String

import java.util.HashMap;

public class Solution {
    public int FirstNotRepeatingChar(String str) {
        if (str==null || str.length()==0) {
            return -1;
        }
        HashMap<Character, Integer> map = new HashMap<>();
        for (int i=0; i<str.length(); i++) {
            char ch = str.charAt(i);
            if (!map.containsKey(ch)) {
                map.put(ch, 1);
            }
            else {
                map.put(ch, map.get(ch)+1);
            }
        }
        int position =0 ;
        for (position=0; position<str.length(); position++) {
            char ch = str.charAt(position);
            if (map.get(ch) == 1) {
                return position;
            }
        }
        return -1;
    }
}
```

## 解法二、使用数组
  
### 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-50.png">
</center>

### AC代码：

```java
public class Solution {
    public int FirstNotRepeatingChar(String str) {
        if (str==null || str.length()==0) {
            return -1;
        }
        char[] chs = str.toCharArray();
        int[] count = new int[123];
        for (int i=0; i<chs.length; i++) {
            count[chs[i]]++;
        }
        for (int i=0; i<chs.length; i++) {
            if (count[chs[i]] == 1) {
                return i;
            }
        }
        return -1;
    }
}
```


## 补充说明： 
   
* 注意：方法`2`中`ASCII`码字母范围`65-90`,`98-122`, 以字母`ASCII`码为下标储存字母出现次数，`count`数组大小至少要`123`。  

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/1c82e8cf713b4bbeb2a5b31cf5b0417c?tpId=13&&tqId=11187&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)