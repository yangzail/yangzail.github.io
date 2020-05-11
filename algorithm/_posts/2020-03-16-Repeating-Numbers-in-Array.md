---
layout: post
title: Sword to Offer-03 数组中重复的数字 ❀
---

* 题目描述：在一个长度为`n`的数组里的所有数字都在`0`到`n - 1`的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。   

* 例如，如果输入长度为`7`的数组`{2,3,1,0,2,5,3}`，那么对应的输出是第一个重复的数字`2`。

## 解题思路：

1、注意到长为`n`数组内数字在`0 ~ n-1`范围；  
2、将数字放在以其大小为下标的位置，如果有重复数字，放置过程会发生冲突；  
3、遍历一次数组，每次将获取到的数字交换到其指定位置；  
4、特殊情况是，该数字已在指定位置`a[i] == i`，此时不处理，当然也不能判别冲突。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-03.png">
</center>

## AC代码：

```java
// Repeated numbers in array

public boolean duplicate(int numbers[],int length,int [] duplication) {
        // if it's a null array, return false
        if (length<=0 || numbers==null){
            return false;
        }
        // traverse the array
        for (int i=0; i<length; i++){
            // if the number is not at the appropriate position, judge
            if (numbers[i] != i) {
                int value = numbers[i];
                // if the number's appropriate position has a same nmuber
                // save the number in an array, and return true
                if (numbers[value] == numbers[i]){
                    duplication[0] = numbers[value];
                    return true;
                }
                // else exchange the number to its appropriate position
                else {
                    exchange(numbers, i, value);
                }
            }
        }
        return false;
    }
    
    
    private void exchange(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }

```
## 补充说明：

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/623a5ac0ea5b4e5f95552655361ae0a8?tpId=13&tqId=11203&rp=4&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&tPage=3)

