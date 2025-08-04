# 395、至少有 K 个重复字符的最长子串
题目难度：mid

题目网址：https://leetcode.cn/problems/longest-substring-with-at-least-k-repeating-characters/description/

代码语言：cpp

## 题解
这是一个很好的理解变长滑动窗口的题目，我们首先考虑常规变长滑动窗口的套路是什么？一般分为最小值和最大值的情况

对于最小值的情况，一个例子是leetcode209.长度最小的子数组。对于这种题，套路是：r不断往右扩展至满足态；到满足态后让l往右缩减至不满足态；答案在缩减时更新；

对于最大值的情况，一个例子是leetcode3.无重复字符的最长子串。对于这种题，套路是：r不断往右扩展至不满足态；到不满足态后让l往右缩减至满足态；答案在扩展时更新；

然而对于这道题目，很显然不满足求最大值的情况，因此我们需要进行一些修改

我们把满足态进行修改，修改为“滑动窗口内的不同字符数小于等于i”，至于i取什么，为了涵盖所有情况，我们直接遍历i从1到26即可，在窗口内我们维护两个变量：1.字符种类数diffcount  2.出现次数不少于k的字符种类数count

这样我们就可以在i取不同值的时候，先将r扩展到不满足态（也就是diffcount>i的情况），然后让l往右进行缩减。那什么时候更新答案呢？其实还是在扩展时更新答案，只不过加上一个限制条件：`count == diffcount && discount <= i`即可

**代码**

C++

```cpp
class Solution {
public:
    int longestSubstring(string s, int k) {
        int res = 0;
        int record[26];
        for (int i = 1; i <= 26; i ++ ) {
            memset(record, 0, sizeof record);
            int diffcount = 0;
            int count = 0;
            int left = 0, right = 0;
            for (; right < s.length(); right ++ ) {
                int index = s[right] - 'a';
                if (record[index] == 0) diffcount ++ ;
                if (record[index] == k - 1) count ++ ;
                record[index] ++ ;
                while (diffcount > i) {
                    index = s[left] - 'a';
                    if (record[index] == 1) diffcount -- ;
                    if (record[index] == k) count -- ;
                    record[index] -- ;
                    left ++ ; 
                }
                if (diffcount == count && diffcount <= i) res = max(res, right - left + 1);
            }
        }
        return res;
    }
};
```
