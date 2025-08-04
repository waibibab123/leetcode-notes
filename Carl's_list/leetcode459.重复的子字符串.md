# 459、重复的子字符串
题目网址：https://leetcode.cn/problems/repeated-substring-pattern/description/

题目难度：easy

代码语言：cpp

## 题解
### 方法一、利用KMP的Next数组
前提知识：熟悉leetcode28的kmp算法原理

首先我们求出s的next数组（下标从1开始），如果`len % (len - next[len]) == 0`那么说明有重复的子字符串，例如abcabcabc，next[9]=6，len-next[len]=3为重复子串的长度，如果能除尽说明s是由该子串重复得到的。

有一种特殊情况是next[len] == 0，对于这种情况，直接返回false即可

**代码**

C++

```cpp
class Solution {
public:
    void getNext(string s, vector<int>& next) {
        int len = s.length() - 1;
        next[0] = next[1] = 0;
        for (int i = 2, j = 0; i <= len; i ++ ) {
            while (j && s[i] != s[j + 1]) j = next[j];
            if (s[i] == s[j + 1]) j ++ ;
            next[i] = j;
        }
    }
    bool repeatedSubstringPattern(string s) {
        s = " " + s;
        int len = s.length() - 1;
        vector<int> next(len + 1, 0);
        getNext(s, next);
        return len % (len - next[len]) == 0 ? next[len] != 0 ? true : false : false;
    }
};
```
