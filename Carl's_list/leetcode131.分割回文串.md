# 131、分割回文串
题目网址：https://leetcode.cn/problems/palindrome-partitioning/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：
* 记录递归路径上的数组：path
* 记录答案数组：res

step2.递归参数：
* s:待分割的字符串
* index：本次要分割的起始位置

step3.边界条件：当index == s.size()说明到达了递归树的叶子结点

step4.确定单次遍历逻辑：从index遍历s，对于每次遍历，在当前遍历的子串是回文串的情况下，首先将此字符串加入path，然后调用递归函数，最后恢复现场

C++
```cpp
class Solution {
public:
    bool check(string str) {
        int l = 0, r = str.size() - 1;
        while (l <= r) {
            if (str[l] != str[r]) return false;
            l ++ , r -- ;
        }
        return true;
    }
    vector<vector<string>> res;
    vector<string> path;
    void dfs(string s, int index) {
        if (index == s.size()) {
            res.push_back(path);
            return;
        }
        for (int i = index; i < s.size(); i ++ ) {
            string str = s.substr(index, i - index + 1);
            if (check(str)) {
                path.push_back(str);
                dfs(s, i + 1);
                path.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        dfs(s, 0);
        return res;
    }
};
```
