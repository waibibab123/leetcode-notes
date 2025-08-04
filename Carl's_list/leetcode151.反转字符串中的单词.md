# 151、反转字符串中的单词
题目网址：https://leetcode.cn/problems/reverse-words-in-a-string/submissions/633216038/

题目难度：mid

代码语言：cpp
## 题解
双指针

分三步：1.去掉多余空格 2.反转字符串 3.反转每个单词；其中1、3两步可以使用双指针解决

C++

```cpp
class Solution {
public:
    void removeExtraSpace(string &s) {
        int slow = 0, fast = 0;
        while (s[fast] == ' ') fast ++ ;
        while (fast < s.length()) {  
            s[slow ++ ] = s[fast ++ ];
            while (fast < s.length() && s[fast] == ' ' && s[fast - 1] == ' ') fast ++ ;
        }
        if (s[fast - 1] == ' ') s.resize(slow - 1);
        else s.resize(slow);
    }
    string reverseWords(string s) {
        removeExtraSpace(s);
        reverse(s.begin(), s.end());
        int slow = 0, fast = 0;
        while (fast < s.length()) {
            while (fast < s.length() && s[fast] != ' ') fast ++ ;
            reverse(s.begin() + slow, s.begin() + fast);
            fast ++ ;
            slow = fast;
        }
        return s;
    }
};
```
