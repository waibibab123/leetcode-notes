# 242、有效的字母异位词
题目网址：https://leetcode.cn/problems/valid-anagram/

题目难度：mid

代码语言：cpp
## 题解
直接哈希，没有什么好说的

C++

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) return false;
        unordered_map<char, int> cnt;
        for (int i = 0; i < s.length(); i ++ ) cnt[s[i]] ++ ;
        for (int i = 0; i < t.length(); i ++ ) {
            if ((cnt[t[i]] -- ) == 0) return false;
        }
        return true;
    }
};
```
