# [剑指 Offer 46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

## 题目

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

```
示例 1:

输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```


提示：

- 0 <= num < 231


## 思路

方法：动态规划

思路：有点类似于那个上楼梯，一次走一步或者两步；很容易得到状态转移方程

## 代码

```golang
func translateNum(num int) int {
    //特殊情况
    if num<10 {
        return 1
    }
    //将数字转化为字符串
    str := strconv.Itoa(num)
    //遍历字符串 将每个数字加入到数组
    arr := make([]int, 0)
    for i := range str {
        arr = append(arr, int(str[i]-'0'))
    }
    m := len(arr)
    //动态规划
    dp := make([]int, m)
    dp[0] = 1
    for i:=1; i<m; i++  {
        if i==1 {
            if isMatch(arr, 1) {
                dp[1] = 2
            }else {
                dp[1] = 1
            }
            continue
        }
        //动态转移
        if isMatch(arr, i) {
            dp[i] = dp[i-1] + dp[i-2]
        }else {
            dp[i] = dp[i-1]
        }
    }
    return dp[m-1]
}

//是否匹配
func isMatch(arr []int, i int) bool{
    if arr[i-1]>2 || arr[i-1]==0 {
        return false
    }
    if arr[i-1]==2 && arr[i]>5 {
        return false
    }
    return true
}
```

