# [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

## 题目

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

```
示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```


提示：

- s.length <= 40000

## 思路

方法：滑动窗口+双指针+哈希表

主要思路：记录一个窗口的长度，这个窗口里面不能有重复的值，所以我们可以用一个哈希表来存储值，遇到重复的值时更新窗口的左边界使得窗口没有重复的值，另外为了避免左边界回到之前的点，这里需要取最大值，比如“abba"。右边界可以直接是遍历字符串的指针。

## 代码

```golang
func lengthOfLongestSubstring(s string) int {
    //滑动窗口+双指针
    left := 0
    result := 0
    hashMap := make(map[rune]int)
    for i, v := range s {
        //窗口中的值重复了
        if _, ok := hashMap[v]; ok {
            //移动窗口 左边 +1是为了避免重复
            //取最大值 是防止窗口左边界 移动之前的位置  “abba”
            left = max(left, hashMap[v]+1)
        }
        hashMap[v] = i
        //更新 窗口的值 取最大
        result = max(result, i-left+1)
    }
    return result
}

func max(x, y int) int {
    if x<y {
        return y
    }
    return x
}
```

