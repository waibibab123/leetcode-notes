# 541、反转字符串2
题目网址：https://leetcode.cn/problems/reverse-string-ii/description/

题目难度：easy

代码语言：cpp

## 题解
没难度直接写即可，下面展示原地操作的代码

C++

```cpp
class Solution {
public:
    string reverseStr(string s, int k) {
        if (s.length() <= k) {
            reverse(s.begin(), s.end());
            return s;
        }
        else if (s.length() < 2 * k) {
            reverse(s.begin(), s.begin() + k);
            return s;
        }
        int i = 0;
        for (; i + 2 * k < s.length(); i += 2 * k) {
            reverse(s.begin() + i, s.begin() + i + k);
        }
        if (i + k > s.length()) reverse(s.begin() + i, s.end());
        else reverse(s.begin() + i, s.begin() + i + k);
        return s;
    }
};
```
