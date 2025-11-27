# 130、被围绕的区域
mid

cpp
## 题解
对于一个'O'，对原始board进行备份并先假定其所在区域被包围，进行bfs搜索确认后，如果没有被包围（即所在区域有的在边界），board恢复，否则继续搜索下一个

C++
```cpp
class Solution {
public:
    constexpr static int dirs[4][2] = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
    int n, m;
    // 判断是否能被围绕
    bool bfs(vector<vector<char>>& board, int x, int y) {
        queue<pair<int, int>> q;
        q.push({x, y});
        while (q.size()) {
            auto t = q.front();
            q.pop();
            int x = t.first, y = t.second;
            for (int i = 0; i < 4; i ++ ) {
                int ax = x + dirs[i][0], ay = y + dirs[i][1];
                if (ax >= 0 && ax < n && ay >= 0 && ay < m && board[ax][ay] == 'O') {
                    if (ax == 0 || ax == n - 1 || ay == 0 || ay == m - 1) return false;
                    board[ax][ay] = 'X';
                    q.push({ax, ay});
                }
            }
        }
        return true;
    }
    void solve(vector<vector<char>>& board) {
        n = board.size(), m = board[0].size();
        for (int i = 1; i < n - 1; i ++ ) {
            for (int j = 1; j < m - 1; j ++ ) {
                if (board[i][j] == 'O') {
                    auto temp = board;
                    board[i][j] = 'X';
                    if (!bfs(board, i, j)) board = temp;
                }
            }
        }
    }
};
```
