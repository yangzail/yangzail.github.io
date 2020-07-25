---
layout: post
title: Sword to Offer-41.2 字符流中第一个不重复的字符 ❀
---

* 题目描述：  
请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符`"go"`时，第一个只出现一次的字符是`"g"`。当从该字符流中读出前六个字符`“google"`时，第一个只出现一次的字符是`"l"`。

* 如果当前字符流不存在出现一次的字符，返回`#`字符。


## 解题思路：

`HashMap`的应用：  
1、将字符流和其中每个字符的出现次数依次存入参数为`Character`和`Integer`的`HashMap`；  
2、新字符插入的时候，若`HashMap`中已存在该字符，将其对应的`Integer+1`，表示其出现的次数`+1`，若不存在该字符，将该字符和`1`添加到`HashMap`；  
3、将字符流依次存入`ArrayList`用于后续遍历查找；  
2、取第一个只出现一次字符的时候，遍历`ArrayList`的元素，将遇到的第一个在`HashMap`中`Integer==1`的元素返回即可。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-41.2.png">
</center>


## AC代码：

```java
// Find the Frst Non-Repeated Character in a Stream

import java.util.HashMap;
import java.util.ArrayList;

public class Solution {
    private HashMap<Character, Integer> map = new HashMap();
    private ArrayList<Character> list = new ArrayList<Character>();
    //Insert one char from stringstream
    public void Insert(char ch) {
        if (map.containsKey(ch)) {
            map.put(ch, map.get(ch)+1);
        }
        else {
            map.put(ch, 1);
        }
        list.add(ch);
    }
  //return the first appearence once char in current stringstream
    public char FirstAppearingOnce() {
        char c = '#';
        for (char key : list) {
            if (map.get(key) == 1) {
                c = key;
                break;
            }
        }
        return c;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/00de97733b8e4f97a3fb5c680ee10720?tpId=13&&tqId=11207&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)