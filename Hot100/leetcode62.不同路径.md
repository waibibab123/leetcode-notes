# 62、不同路径
难度：mid

题目网址：https://leetcode.cn/problems/unique-paths/

代码语言：cpp

## 题解
### 方法一、动态规划
step1、状态表示：dp[i][j]表示从左上角到达位置(i,j)的不同路径数量

step2、状态转移：任意一个位置(i,j)(其中`i != 0 && j != 0`)，可以从上面到达，也可以从左面到达，因此`dp[i][j] = dp[i - 1][j] + dp[i][j - 1]`

step3、边界处理：当`i == 0 || j == 0`时，位置(i,j)只能从一个方向到达，因此这些位置的dp[i][j]必然为1

C++

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 0));
        for (int i = 0; i < m; i ++ ) dp[i][0] = 1;
        for (int i = 0; i < n; i ++ ) dp[0][i] = 1;
        for (int i = 1; i < m; i ++ ) {
            for (int j = 1; j < n; j ++ ) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```
