# 909、蛇形棋
mid

cpp
## 题解
bfs
```cpp

class Solution {
public:
    using PII = pair<int, int>;
    int n;
    //把位置号转换为坐标
    PII pos2xy(int pos) {
        pos -- ;
        int x = n - pos / n - 1;
        int y = pos % n;
        if ((pos / n) % 2 == 1) y = n - y - 1;
        return {x, y};
    }
    int snakesAndLadders(vector<vector<int>>& board) {
        unordered_map<int, bool> visited;
        n = board.size();
        queue<PII> q;//{坐标，筛子次数}
        q.push({1, 0});
        visited[1] = true;
        // for (int i = 1; i <= n * n; i ++ ) cout << pos2xy(i).first <<" " << pos2xy(i).second<< endl;
        while (q.size()) {
            auto t = q.front();
            q.pop();
            int pos = t.first;
            // cout << pos << endl;
            int cnt = t.second;
            for (int i = pos + 1; i <= pos + 6; i ++ ) {
                if (i > n * n) break;
                auto xy = pos2xy(i);
                int dest = board[xy.first][xy.second];
                int nextpos;
                if (dest != -1) nextpos = dest;
                else nextpos = i;
                if (nextpos == n * n) return cnt + 1;
                if (visited[nextpos] == false) {
                    visited[nextpos] = true;
                    q.push({nextpos, cnt + 1});
                }
            }
        }
        return -1;
    }
};
```
