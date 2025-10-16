# 58、最后一个单词的长度
题目网址：https://leetcode.cn/problems/length-of-last-word/submissions/671023775/?envType=study-plan-v2&envId=top-interview-150

题目难度：easy

代码语言：cpp
## 题解
方法一、双指针

思路：先通过双指针算法去掉冗余空格，然后直接计算最后一个单词的长度

C++
```cpp
class Solution {
public:
    int lengthOfLastWord(string s) {
        s = removeExtraSpace(s);
        cout << s;
        return s.find(" ") == -1 ? s.length() : (s.length() - s.rfind(" ") - 1);
    }
    string removeExtraSpace(string s) {
        int slow = 0, fast = 0;
        while (fast < s.size() && s[fast] == ' ') fast ++ ;
        for (; fast < s.size(); fast ++ ) {
            if (fast - 1 >= 0 && s[fast - 1] == s[fast] && s[fast] == ' ') continue;
            else s[slow ++ ] = s[fast];
        }
        cout << s << endl;
        if (slow - 1 >= 0 && s[slow - 1] == ' ') s.resize(slow - 1);
        else s.resize(slow);
        return s;
    }
};
```

方法二、使用stringstream

这个方法需要注意：由于 getline 在遇到连续空格时会生成空字符串，因此需要过滤掉这些空字符串，只保留有效的单词。

C++
```cpp
class Solution {
public:
    int lengthOfLastWord(string s) {
        stringstream ss(s);
        vector<string> tokens;
        string token;
        while (getline(ss, token, ' ')) {
            if (!token.empty())
            tokens.push_back(token);
        }
        return tokens.back().length();
    }
};
```
