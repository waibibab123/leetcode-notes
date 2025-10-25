# 76、最小覆盖子串
题目难度：hard

代码语言：cpp
## 题解
变长滑动窗口：
* 1.入窗
* 2.更新&出窗

第一个版本，我是这样写的：
```cpp
class Solution {
public:
    bool isContain(unordered_map<char, int> &curFreq, unordered_map<char, int> &targetFreq) {
        for (auto item : targetFreq) {
            if (item.second > curFreq[item.first]) return false;
        }
        return true;
    }
    string minWindow(string s, string t) {
        unordered_map<char, int> targetFreq;
        string res;
        int s_len = s.length();
        int t_len = t.length();
        for (int i = 0; i < t_len; i ++ ) targetFreq[t[i]] ++ ;
        unordered_map<char, int> curFreq;
        int l = 0, r = 0;
        for (; r < s_len; r ++ ) {
            //1.入窗
            curFreq[s[r]] ++ ;
            //2.更新&出窗
            while (isContain(curFreq, targetFreq)) {
                if (res.length() > (r - l + 1) || res == "") res = s.substr(l, r - l + 1);
                curFreq[s[l ++ ]] -- ;
            }
        }
        return res;
    }
};
```

但是会存在内存超限的问题，这是因为在更新&出窗的阶段，在不断地生成子字符串，实际上这个过程最好只生成一次，因此优化为：

```cpp
class Solution {
public:
    bool isContain(unordered_map<char, int> &curFreq, unordered_map<char, int> &targetFreq) {
        for (auto item : targetFreq) {
            if (item.second > curFreq[item.first]) return false;
        }
        return true;
    }
    string minWindow(string s, string t) {
        unordered_map<char, int> targetFreq;
        string res;
        int s_len = s.length();
        int t_len = t.length();
        for (int i = 0; i < t_len; i ++ ) targetFreq[t[i]] ++ ;
        unordered_map<char, int> curFreq;
        int l = 0, r = 0;
        for (; r < s_len; r ++ ) {
            //1.入窗
            curFreq[s[r]] ++ ;
            //2.更新&出窗
            if (isContain(curFreq, targetFreq)) {
                while (isContain(curFreq, targetFreq)) curFreq[s[l ++ ]] -- ;
                if (res.length() > (r - l + 2) || res == "") res = s.substr(l - 1, r - l + 2);
            }
        }
        return res;
    }
};
```
