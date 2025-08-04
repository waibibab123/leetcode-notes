# 28、找出字符串中第一个匹配项的下标
题目网址：https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/description/

题目难度：easy

代码语言：cpp

## 题解
本题可以使用KMP算法，这个算法较为复杂，详细可以参考我的csdn博客文章：https://blog.csdn.net/m0_63222058/article/details/144618382?spm=1001.2014.3001.5501

力扣代码

C++

```cpp
class Solution {
public:
    void getNext(string needle, vector<int>& next) {
        int len = needle.length() - 1;
        next[0] = next[1] = 0;
        for (int i = 2, j = 0; i <= len; i ++ ) {
            while (j && needle[i] != needle[j + 1]) j = next[j];
            if (needle[i] == needle[j + 1]) j ++ ;
            next[i] = j;
        }
    }
    int strStr(string haystack, string needle) {
        haystack = " " + haystack;
        needle = " " + needle;
        vector<int> next(needle.length(), 0);
        getNext(needle, next);
        int len1 = haystack.length() - 1;
        int len2 = needle.length() - 1;
        for (int i = 1, j = 0; i <= len1; i ++ ) {
            while (j && haystack[i] != needle[j + 1]) j = next[j];
            if (haystack[i] == needle[j + 1]) j ++ ;
            if (j == len2) {
                return i - j;
            }
        }
        return -1;
    }
};
```
