---
layout: post
title: Sword to Offer-37 序列化二叉树 ❀❀
---

* 题目描述：  
请实现两个函数，分别用来序列化和反序列化二叉树。  

* 二叉树的序列化是指：  
把一棵二叉树按照某种遍历方式的结果以某种格式保存为字符串，从而使得内存中建立起来的二叉树可以持久保存。序列化可以基于先序、中序、后序、层序的二叉树遍历方式来进行修改，序列化的结果是一个字符串，序列化时通过某种符号表示空节点`（#）`，以 `！` 表示一个结点值的结束`（value!）`。  

* 二叉树的反序列化是指：  
根据某种遍历顺序得到的序列化字符串结果`str`，重构二叉树。

* 例如，我们可以把一个只有根节点为`1`的二叉树序列化为`"1,"`，然后通过自己的函数来解析回这个二叉树。

## 解题思路：

1、按照题述进行序列化：  
一个简单二叉树输出格式应为`“1！2！#！#！3！#！#！”`，即每个叶子结点需要指向两个空值结点,形如`“leaf.val！#！#！”`；  

2、序列化选用前序遍历:    
树为空对应的序列为`#！`,否则递归序列化，给序列前后添加`“root.val！”`,左子树序列和右子树序列；  

3、反序列化前序序列：  
(1) 先将序列`String`划分成由每个结点的实际`val`组成的字符串数组，注意此处用`split`方法划分后，得到的是字符而不是数字，使用序号`index`来标记当前是第几个结点;  
(2) 反序列化的递归方法，退出条件为`index >= 结点个数`（即字符串数组长度）;  
(3) 若当前节点不为`"#"`，即不为空节点，新建一个根结点root用来记录其值并返回，再将当前结点的左右指针指向对左右子树分别继续反序列化返回的根结点。


## 问题图解：

<center>
    <img src="/assets/img/blog/sword-offer-37.png">
</center>


## AC代码：

```java
// Serialize and Deserialize Binary Tree

import java.util.List;
import java.util.LinkedList;
import java.util.Arrays;

public class Solution {
    private String serial = "";
    private int index = -1;
    //空值返回"#!"，正常值返回"val!"

    public String Serialize(TreeNode root) {
        if (root == null) {
            serial += "#!";
        }
        else {
            serial += root.val + "!";
            serial = Serialize(root.left);
            serial = Serialize(root.right);
        }
        return serial;
    }
    
    public TreeNode Deserialize(String str) {
        String[] nodes = str.split("!");
        int len = nodes.length;
        
        index++;
        if (index >= len) {
            return null;
        }
        TreeNode root = null;
        if (!nodes[index].equals("#")) {
            int val = Integer.valueOf(nodes[index]);
            root = new TreeNode(val);
            root.left = Deserialize(str);
            root.right = Deserialize(str);
        }
        
        return root;
    }
}
```

## 补充说明：

* 注意：
`String`类型的变量`serial`一定要初始化为`""`,否则会自动初始化为`null`；  `null`是不指向任何地方，无类型，`""`是指向某个`String`类型，只是还没有具体元素，否则会初始化失败，报变量格式错误`NumberFormatExcetion`。   


* 这里是[牛客编码链接](https://www.nowcoder.com/practice/cf7e25aa97c04cc1a68c8f040e71fb84?tpId=13&&tqId=11214&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)