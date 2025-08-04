# 455、分发饼干
贪心

C++
```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        int res = 0;
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int index = s.size() - 1;
        for (int i = g.size() - 1; i >= 0; i -- ) {
            if (index < 0) break;
            if (g[i] <= s[index]) {
                res ++ ;
                index -- ;
            }
        }
        return res;
    }
};
```
