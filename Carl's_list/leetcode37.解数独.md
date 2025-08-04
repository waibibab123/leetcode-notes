# 37、解数独
回溯

遍历board的每个元素，如果为'.'，就尝试1到9每个数填在这里是否成立，如果成立，进行递归继续填充下一个'.'，如果某个格子1-9就不成立，那么就返回false

C++

```cpp
class Solution {
public:
    bool check(vector<vector<char>>& board, int x, int y, char k) {
        for (int i = 0; i < 9; i ++ ) {
            if (board[x][i] == k) return false;
        }
        for (int i = 0; i < 9; i ++ ) {
            if (board[i][y] == k) return false;
        }
        int a = x / 3;
        int b = y / 3;
        for (int i = 0; i < 3; i ++ ) {
            for (int j = 0; j < 3; j ++ ) {
                if (board[a * 3 + i][b * 3 + j] == k) return false;
            }
        }
        return true;
    }
    bool dfs(vector<vector<char>>& board) {
        for (int i = 0; i < board.size(); i ++ ) {
            for (int j = 0; j < board[0].size(); j ++ ) {
                if (board[i][j] == '.') {
                    for (char k = '1'; k <= '9'; k ++ ) {
                        if (check(board, i, j, k)) {
                            board[i][j] = k;
                            if (dfs(board)) return true;
                            board[i][j] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    void solveSudoku(vector<vector<char>>& board) {
        dfs(board);
    }
};
```
