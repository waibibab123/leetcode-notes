# 344、反转字符串
题目网址：https://leetcode.cn/problems/reverse-string/description/

题目难度：easy

代码语言：cpp

## 题解
唯一要说明的是这个交换两个数的方法使用了位运算替代了swap函数

```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        for (int i = 0, j = s.size() - 1; i < s.size() / 2; i ++, j -- ) {
            s[i] ^= s[j];
            s[j] ^= s[i];
            s[i] ^= s[j];
        }
    }
};
```
