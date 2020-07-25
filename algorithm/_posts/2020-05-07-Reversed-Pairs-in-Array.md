---
layout: post
title: Sword to Offer-51 数组中的逆序对 ❀❀
---

* 题目描述：  
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数`P`。并将`P`对`1000000007`取模的结果输出。 即输出`P%1000000007`。

* 输入描述：  
题目保证输入的数组中没有的相同的数字，数据范围：  
对于`%50`的数据,`size<=10^4`  
对于`%75`的数据,`size<=10^5`  
对于`%100`的数据,`size<=2*10^5`  


## 解题思路：

（在数据量较大情况下，用类似冒泡排序的双重循环进行逆序对判断会超时，笑~）  
  
所以只能考虑时间复杂度更低的排序算法，如归并排序：  
1、采用递归方法进行子序列的划分和归并；  
2、归并时，位于前面的子数组`arr[i~mid]`元素有序，若`arr[i]>arr[j]`（位于后面的子数组的第一个元素），那么它后面的元素也都`>arr[j]`，即`arr[i~mid]`元素都与`arr[j]`元素组成逆序对，其个数为`(mid -i +1)`，统计整个排序过程中的这个值的总和即为原数组所有逆序对数。

## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-51.png">
</center>


## AC代码：

```java
// Reversed Pairs of Numbers in Array （Merge Sort）

public class Solution {
    
    private long count = 0;
    private int[] tmpArr;
    
    public int InversePairs(int [] array) {
        if (array==null || array.length==0) {
            return 0;
        }
        tmpArr = new int[array.length];  // 初始化临时数组
        divide(array, 0, array.length-1);
        return (int)(count%1000000007);
    }
    
    private void divide(int[] arr, int low, int high) {
        if (low >= high) {
            return;
        }
        int mid = (low + high) / 2;
        // 递归划分
        divide(arr, low, mid);
        divide(arr, mid + 1, high);
        // 归并排序
        mergeSort(arr, low, mid, high);
    }
    
    private void mergeSort(int[] arr, int low, int mid, int high) {
        int i = low, j = mid + 1, k = low;
        while (i<=mid && j<=high) {
            if (arr[i] <= arr[j]) {
                tmpArr[k++] = arr[i++];
            }
            else {
                tmpArr[k++] = arr[j++];
                count += mid-i+1;
            }
        }
        while (i <= mid) {
            tmpArr[k++] = arr[i++];
        }
        while (j <= high) {
            tmpArr[k++] = arr[j++];
        }
        //  排序完一小部分就拷贝回原数组
        for (k=low; k<=high; k++) {
            arr[k] = tmpArr[k];
        }
    }
}
```


## 补充说明： 
   
* 注意：  
    1、此处用`long`类型变量`count`来记录逆序对数目，用`int`只`AC50%`，要求的返回类型`count%1000000007`为`int`类型，求余后类型转换为`int`即可；  

   2、归并排序的归并完成时，需要将排好的`tmp`数组中的值拷贝回原数组对应位置，原因是为了保证下一次归并过程中，原数组中待合并的两个子数组依旧有序。    

* 这里是[牛客编码链接](https://www.nowcoder.com/practice/96bd6684e04a44eb80e6a68efc0ec6c5?tpId=13&&tqId=11188&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)