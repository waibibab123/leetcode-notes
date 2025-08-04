# 64、最小路径和
难度：mid

题目网址：https://leetcode.cn/problems/minimum-path-sum/description/

代码语言：cpp

## 题解
### 方法一、动态规划
step1.状态表示：dp[i][j]表示从左上角到(i,j)路径上的数字总和最小值

step2.状态转移：`dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]`

step3.边界处理：当`i == 0 || j == 0`时，首先必然有：`dp[0][0] == grid[0][0]`，其次，(i,j)只能从一个方向到达，因此这部分应该初始化：`dp[i][0] = dp[i - 1][0] + grid[i][0]`和`dp[0][i] = dp[0][i - 1] + grid[0][i]`

C++

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        vector<vector<int>> dp(n, vector<int>(m, 0x3f3f3f3f));
        dp[0][0] = grid[0][0];
        for (int i = 1; i < n; i ++ ) dp[i][0] = grid[i][0] + dp[i - 1][0];
        for (int i = 1; i < m; i ++ ) dp[0][i] = grid[0][i] + dp[0][i - 1];
        for (int i = 1; i < n; i ++ ) {
            for (int j = 1; j < m; j ++ ) {
                dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }
        return dp[n - 1][m - 1];
    }
};
```
