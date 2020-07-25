---
layout: post
title: Sword to Offer-38 字符串的排列 ❀❀❀
---

* 题目描述：  
输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串`“abc”`,则打印出由字符`a`,`b`,`c`所能排列出来的所有字符串`abc`,`acb`,`bac`,`bca`,`cab`和`cba`。

* 输入描述：  
输入一个字符串,长度不超过`9`(可能有字符重复),字符只包括大小写字母。  

## 解题思路：

1、取第一个字符与后面每个字符交换作为`n-1`个字符串，对这`n-1`个字符串分别取它们的第一个字符与后面每个字符做交换，以此类推可得出所有可能的排列情况；  
2、对于每个字符，后面的操作类似，因此可用递归求解；  
3、递归退出条件为递归到了最后一个元素，此时出现了一种排列，若不与以前的重复就可保留；  
4、每次递归完成后，需要将原来交换的元素换回来，防止之后交换时使用的不是原本的第一个字符；  
5、比如，对于字符串`“abcd”`，`“a”`与`“b”`交换的时候可得到的字符串为`“baxx”`，在该条分支遍历完之后应该轮到`“a”`和`“c”`互换，所以要先将`“a”`和`“b”`字符交换回来，再换第一个字符`“a”`和第三个字符`“c”`。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-38.png">
</center>


## AC代码：

```java
// Find All Arrangement of A String

import java.util.ArrayList;
import java.util.Collections;

public class Solution {
    public ArrayList<String> Permutation(String str) {
        ArrayList<String> res = new ArrayList<>();
        if (str!=null && str.length()>0) {
            corePermutation(str.toCharArray(), 0, res);
            Collections.sort(res);  //不按顺序输出可能不匹配输出用例
        }
        return res;
    }
    
    private void corePermutation(char[] chs, int i, ArrayList<String> list) {
        if (i == chs.length-1) {
            String strTmp = String.valueOf(chs);  //将chs[]转换为字符串
            if (!list.contains(strTmp))
                list.add(strTmp);
        }
        else {
            for (int j=i; j<chs.length; j++) {
                swap(chs, i, j);
                corePermutation(chs, i+1, list);
                swap(chs, i, j);
            }
        }
    }
    
    private void swap(char[] chs, int i, int j) {
        char tmp = chs[i];
        chs[i] = chs[j];
        chs[j] = tmp;
    }
}
```

## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/fe6b651b66ae47d7acce78ffdd9a96c7?tpId=13&&tqId=11180&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)