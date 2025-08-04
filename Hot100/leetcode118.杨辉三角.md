# 118、杨辉三角
难度：easy

代码语言：cpp

题目网址：https://leetcode.cn/problems/pascals-triangle/description/

## 解法
### 方法一、动态规划
状态表示：$`dp[i][j]`$表示第i行第j个数的值

状态转移：由题意知：$`dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j]`$，但是要注意对边界条件特殊判断

边界处理：为了后续的状态转移能够顺利进行，我们初始化杨辉三角的第一行:`dp[i] = vector<int>{1}`

## 代码
C++

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> dp;
        dp.push_back(vector<int>{1});
        if (numRows == 1) return dp;
        for (int i = 1; i < numRows; i ++ ) {
            vector<int> temp;
            for (int j = 0; j <= i; j ++ ) {
                int x = 0;
                if (j > 0) x += dp[i - 1][j - 1];
                if (j < i) x += dp[i - 1][j];
                temp.push_back(x);
            }
            dp.push_back(temp);
        }
        return dp;
    }
};
```
