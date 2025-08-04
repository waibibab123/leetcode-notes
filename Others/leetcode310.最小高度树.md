# 310、最小高度树
题目难度：mid

题目网址：https://leetcode.cn/problems/minimum-height-trees/description/

代码语言：cpp
## 题解
### 方法一、bfs
什么点作根节点会让整棵树的高度最低？答案是尽量靠“里面”的节点。这道题可以看作是拓扑排序的变形，先让入度为1的（最外面的点）入队，一层一层地往里找，直到找到最里面的一层点。

**代码**

C++

```cpp
class Solution {
public:
    const static int N = 50010;
    int e[N];
    int ne[N];
    int h[N];
    int d[N];
    int idx;
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        if (edges.size() == 0) return vector<int>{0};
        memset(h, -1, sizeof h);
        idx = 0;
        for (int i = 0; i < edges.size(); i ++ ) {
            int a = edges[i][0], b = edges[i][1];
            add(a, b);
            add(b, a);
            d[a] ++ ;
            d[b] ++ ;
        }
        queue<int> q;
        vector<int> res;
        for (int i = 0; i < n; i ++ ) {
            if (d[i] == 1) {
                q.push(i);
            }
        }
        while (q.size()) {
            res.clear();
            int size = q.size();
            for (int i = 1; i <= size; i ++ ) {
                auto t = q.front();
                res.push_back(t);
                q.pop();
                for (int j = h[t]; j != -1; j = ne[j]) {
                    int k = e[j];
                    if ((-- d[k]) == 1) {
                        q.push(k);
                    }
                }
            }
        }
        return res;
    }
    void add(int a, int b) {
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx ++ ;
    }
};
```
