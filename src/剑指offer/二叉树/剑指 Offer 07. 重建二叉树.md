# [剑指 Offer 07. 重建二叉树](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

## 题目

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

```golang
示例 1:
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

示例 2:
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

**限制：**

- 0 <= 节点个数 <= 5000

## 思路

方法：递归

主要思路：首先根节点即为前序遍历的第一个元素；然后遍历后序遍历结果得到 索引，这个索引左右两边分别是左右子树；因为左右子树长度是固定的，所以可以根据这个索引在前序遍历结果 找到左右子树，最后递归左右子树，返回根节点。

细节：索引需要加一；前序遍历结果大于0

## 代码

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
    //递归 
    //边界条件
    if len(preorder)==0 {
        return nil
    }
    //根节点 为前序遍历的 第一个元素
    root := &TreeNode{preorder[0], nil, nil}
    //遍历 中序遍历结果 得到索引值
    i := 0
    for ;i<len(inorder); i++ {
        //等于根节点值
        if inorder[i] == preorder[0] {
            break
        }
    }
    //递归得到左右子树

    //找到索引 索引左边的元素长度 即为左子树长度 映射到前序遍历结果
    //索引右边 右子树
    //左子树长度加一
    root.Left = buildTree(preorder[1:i+1], inorder[:i])
    root.Right = buildTree(preorder[i+1:], inorder[i+1:])
    return root
}
```

