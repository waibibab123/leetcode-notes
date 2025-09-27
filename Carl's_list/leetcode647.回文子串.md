# leetcode647、回文子串
题目网址：https://leetcode.cn/problems/palindromic-substrings/description/

题目难度：mid

代码语言：cpp
## 题解
二维数组dp[i][j]，用来表示字符串从第 i 个字符到第 j 个字符组成的子串是否是回文串

判断s[i-1]和s[j-1]是否相等（减 1 是因为字符串下标从 0 开始）：

如果相等：
* 若子串长度小于等于 2（j-i≤1），直接是回文串
* 若子串更长，则看去掉首尾字符后的子串dp[i+1][j-1]是否是回文串

只要满足回文条件，就计数加 1
最后返回计数结果 res，就是所有回文子串的总数

注意因为dp[i][j]是通过dp[i+1][j-1]推到的，因此i这个维度需要倒序遍历

C++
```cpp
class Solution {
public:
    int countSubstrings(string s) {
        int res = 0;
        int n = s.length();
        vector<vector<bool>> dp(n + 1, vector<bool>(n + 1, false));
        for (int i = n; i >= 1; i -- ) {
            for (int j = i; j <= n; j ++ ) {
                if (s[i - 1] == s[j - 1]) {
                    if (j - i <= 1) {
                        dp[i][j] = true;
                        res ++ ;
                    } else if (dp[i + 1][j - 1] == true) {
                        dp[i][j] = true;
                        res ++ ;
                    }
                }
            }
        }
        return res;
    }
};
```
