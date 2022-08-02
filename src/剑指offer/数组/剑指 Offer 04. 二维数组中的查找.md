## [剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

## 题目

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```golang
示例:
现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

限制：

- 0 <= n <= 1000

- 0 <= m <= 1000

## 思路

方法：类比

主要思路：类似于二叉搜索树，将左下角或者右上角作为“根节点”；大于或者小于移动一列或者一行

细节：结束条件是 i>=0；可以等于，因为可能根节点就是要找的元素

## 代码

```golang
func findNumberIn2DArray(matrix [][]int, target int) bool {
    if len(matrix)==0 {
        return false
    }
    //类似于 二叉搜索树
    i, j := 0, len(matrix[0])-1
    //将最 右上角 元素 作为“根节点”
    for i<len(matrix) && j>=0 {
        if target==matrix[i][j] {
            return true
        }else if target>matrix[i][j] { 
            i++
        }else {
            j--
        }
    }
    return false
}
```

## 总结

- 复杂度：时间复杂度为 O(m+n)；空间复杂度为 O(1)
- [参考链接](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/solution/mian-shi-ti-04-er-wei-shu-zu-zhong-de-cha-zhao-zuo/)