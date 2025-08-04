# 63、不同路径2
题目网址：https://leetcode.cn/problems/unique-paths-ii/

题目难度：mid

代码语言：cpp
## 题解
动态规划

设`dp[i][j]`是到达(i,j)的路线总数，刚开始可以全部初始化为0，仅起点初始化为1（但起点一定不是障碍），当（i,j）是障碍，`dp[i][j]`必为0，当（i,j）不是障碍时，转移方程为：`dp[i][j] = (obstacle[i - 1][j] == 1 ? 0 : dp[i - 1][j]) + (obstacle[i][j - 1] == 1 ? 0 : dp[i][j - 1])`

C++
```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if (obstacleGrid[0][0] == 1) return 0;
        int m = obstacleGrid.size(), n = obstacleGrid[0].size();
        vector<vector<int>> dp(m, vector<int>(n, 0));
        dp[0][0] = 1;
        for (int i = 1; i < m; i ++ ) dp[i][0] = (obstacleGrid[i][0] == 0) ? dp[i - 1][0] : 0;
        for (int i = 1; i < n; i ++ ) dp[0][i] = (obstacleGrid[0][i] == 0) ? dp[0][i - 1] : 0;
        for (int i = 1; i < m; i ++ ) {
            for (int j = 1; j < n; j ++ ) {
                if (obstacleGrid[i][j] == 1) {
                    dp[i][j] = 0;
                    continue;
                }
                if (obstacleGrid[i - 1][j] == 0) dp[i][j] += dp[i - 1][j];
                if (obstacleGrid[i][j - 1] == 0) dp[i][j] += dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```
