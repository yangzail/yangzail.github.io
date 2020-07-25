---
layout: post
title: Sword to Offer-61 扑克牌顺子 ❀❀
---

* 题目描述：  
LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有`2`个大王,`2`个小王(一副牌原本是`54`张^_^)...他随机从中抽出了`5`张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！`“红心A,黑桃3,小王,大王,方片5”`,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且`A`看作`1`,`J`为`11`,`Q`为`12`,`K`为`13`。上面的`5`张牌就可以变成`“1,2,3,4,5”`(大小王分别看作`2`和`4`),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何， 如果牌能组成顺子就输出`true`，否则就输出`false`。为了方便起见,你可以认为大小王是`0`。

## 解题思路：

1、遍历一遍记下大小王（题设为`0`）个数；  
2、对抽到的牌进行一个从小到大的排序；  
3、从不为`0`的数字开始两两判断，两数字之间差`k`个数：  
（1）`k=1`这两个数是顺子，继续判断；  
（2）`1<k<=癞子个数`，就修改剩余大小王个数，当该值`<0`，直接返回`false`；  
（3）`k>癞子个数`，直接返回`false`，不可能组成顺子；  
（4）如果能遍历完而没有返回，说明是顺子没错，返回`true`。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-61.png">
</center>


## AC代码：

```java
// Judge Poker Straight With King Replace Any Number

public class Solution {
    public boolean isContinuous(int [] numbers) {
        if (numbers.length != 5) {
            return false;
        }
        int superNum = 0;  // 癞子个数
        for (int i=0; i<numbers.length; i++) {
            if (numbers[i] == 0) {
                superNum++;
            }
        }
        // 从小到大排序
        for (int i=0; i<numbers.length; i++) {
            for (int j=i+1; j<numbers.length; j++) {
                if (numbers[i] > numbers[j]) {
                    int tmp = numbers[i];
                    numbers[i] = numbers[j];
                    numbers[j] = tmp;
                }
            }
        }
        for (int i=superNum; i<numbers.length-1; i++) {
            if (numbers[i+1]-numbers[i] == 1) {
                continue;
            }
            else if (numbers[i+1]-numbers[i]>1 && numbers[i+1]-numbers[i]-1<=superNum) {
                superNum -= numbers[i+1]-numbers[i]-1;
                if (superNum < 0) {
                    return false;
                }
            }
            else {
                return false;
            }
        }
        return true;
    }
}
```


## 补充说明： 

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/762836f4d43d43ca9deb273b3de8e1f4?tpId=13&&tqId=11198&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)