# 5、最长回文子串
题目难度：mid

题目网址：https://leetcode.cn/problems/longest-palindromic-substring/

代码语言：cpp

## 题解
### 方法一、动态规划

step1.状态表示：$`dp[i][j]`$表示字符串s从下标i到下标j的子串是否为回文子串，若是，则`dp[i][j] == true`

step2.状态转移：

* 若`s[i] != s[j]` ，则`dp[i][j] = false`
* 若`s[i] == s[j]` ，则：
  * 若`j - i <= 1` ，则`dp[i][j] = true`，因为单个字符必然是回文子串，对于两个字符的串，如果两个字符相同，则也是回文子串
  * 若`j - i > 1 && dp[i + 1][j - 1] == true`，则则`dp[i][j] = true`，比如ababa为回文串的前提是bab位回文串

step3.边界处理：直接让dp数组的所有元素初始化为false即可

step4.遍历顺序：注意`dp[i][j]`状态转移主要靠的是：`dp[i + 1][j - 1]`，对于i来说，是i + 1 --推出--> i，因此i的遍历必须是逆向，即从s.length() - 1遍历到0，而j由于是j - 1 --推出--> j，因此j的遍历正向即可

**代码**

C++ 

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int len = s.length();
        string res = "";
        vector<vector<bool>> dp(len, vector<bool>(len, false));
        for (int i = len - 1; i >= 0; i -- ) {
            for (int j = i; j < len; j ++ ) {
                if (s[i] != s[j]) dp[i][j] = false;
                else {
                    if (j - i <= 1) {
                        dp[i][j] = true;
                        if (j - i + 1 > res.length()) {
                            res = s.substr(i, j - i + 1);
                        }
                    } else if (dp[i + 1][j - 1] == true) {
                        dp[i][j] = true;
                        if (j - i + 1 > res.length()) {
                            res = s.substr(i, j - i + 1);
                        }
                    }
                }
            }
        }
        return res;
    }
};
```
