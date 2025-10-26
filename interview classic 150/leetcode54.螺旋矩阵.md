# 54、螺旋矩阵
题目难度：mid

代码语言：cpp
## 题解
对于这种模拟题，都可以像leetcode6.Z字形变换那样，定义一个目前的坐标，然后想办法去更新这个坐标值，对于这道题，可以定义上下左右四个方向，原来的时候这个坐标的方向是朝右的，当满足以下两个条件时，需要进行方向的调整，1.马上要超界了 2.之前走过这里  对于第一个条件，只是一个简单的边界判断，对于第二个条件
可以定义一个标记数组visited去记录每个已经访问过的坐标位置

C++
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        vector<pair<int, int>> direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};//定义四个方向，右、下、左、上
        int curDir = 0;//刚开始朝右走
        vector<int> res(m * n, 0);
        int x = 0, y = 0;
        for (int i = 0; i < res.size(); i ++ ) {
            //装入路径
            res[i] = matrix[x][y];
            visited[x][y] = true;
            //寻找下一步的坐标，如果已经走到最后一个位置，那就不用找
            if (i == res.size() - 1) break;
            int temp_x = x + direction[curDir].first, temp_y = y + direction[curDir].second;
            while (!(temp_x >= 0 && temp_x < m && temp_y >= 0 && temp_y < n && !visited[temp_x][temp_y])) {
                curDir = (curDir + 1) % 4;
                temp_x = x + direction[curDir].first, temp_y = y + direction[curDir].second;
            }
            x = temp_x;
            y = temp_y;
        }
        return res;
    }
};
```
