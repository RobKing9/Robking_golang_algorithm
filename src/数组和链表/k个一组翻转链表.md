# [25. K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

## 题目

给你链表的头节点 head ，每 k 个节点一组进行翻转，请你返回修改后的链表。

k 是一个正整数，它的值小于或等于链表的长度。如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

```
输入：head = [1,2,3,4,5], k = 2
输出：[2,1,4,3,5]

输入：head = [1,2,3,4,5], k = 3
输出：[3,2,1,4,5]
```

**提示：**

- 链表中的节点数目为 `n`
- `1 <= k <= n <= 5000`
- `0 <= Node.val <= 1000`

## 思路

方法：迭代

主要思路：遍历链表；获得每组的头部和尾部（函数封装），分组遍历，将每组都翻转过来（函数封装）；

之后就是把每一组看做一个整体，改变每组的外部边；

细节：每组看做整体的时候，需要维护last，因为翻转的时候被改过；需要添加一个保护节点（哑巴节点），指向head；防止 开始的那一组没有last；翻转head到end的时候，注意k=1的情况，直接返回；最后避免刚好head=end导致没有翻转，end.Next = last 翻转最后一个节点

优化：

## 代码

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseKGroup(head *ListNode, k int) *ListNode {
    //如果节点总数<k
    // length := 0
    // for ;head!=nil; head=head.Next {
    //     length++
    // }
    // if k>length {
    //     return head
    // }
    protect := &ListNode{Val:0}
    protect.Next = head
    //维护上一个节点  需要添加保护节点? --防止为空
    last := protect
    //遍历链表
    for head!=nil {
        //第一组前k个翻转 怎么翻转？
        //翻转后接哪里？ 怎么确认有几个k
        //怎么处理外部的边的改变
        //分组遍历 获得每组的头部和尾部


        end := getEnd(head, k)

        //end为空
        if end==nil {
            break
        }
        nextGroupHead := end.Next
        //翻转 head 到 end k-1条边
        reverse(head, end)
        //本组新head（上一组的end）和上一组建立联系
        last.Next = end
        //本组的新结尾（head）和下一组建立联系
        //原本下一组的head是 本组的 end.Next 但是由于前面翻转了 所以需要维护
        head.Next = nextGroupHead
        //整体上 last和head往下移动一位
        last = head
        head = nextGroupHead
    }
    return protect.Next
}

//获得每组的最后一个节点
func getEnd(head *ListNode, k int) *ListNode {
    for head!=nil {
        k--
        if k==0 {
            break
        }
        head = head.Next
    }
    return head
}

//翻转从head到end，第一个节点不需要处理，直接从下一个开始
func reverse(head, end *ListNode) {
    //head和end相等 k=1
    if head==end {
        return 
    }
    //忽略第一个节点，边不需要改变
    pre := head
    head = head.Next
    for head!=end {
        next := head.Next
        head.Next = pre
        pre = head
        head = next
    }
    //防止 最后刚好 head=end 没有翻转
    end.Next = pre
}




```

