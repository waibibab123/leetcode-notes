# 452、用最少数量的箭引爆气球
贪心

先将区间按照右端点排序，第一个射箭点选择第一个区间的右端点b，然后从第二个区间开始遍历，如果第k个区间的左端点大于b，就再射出一个箭选择第k个区间的右端点

C++
```cpp
class Solution {
public:
    static bool cmp(vector<int> a, vector<int> b) {
        if (a[1] != b[1]) return a[1] < b[1];
        else return a[0] < b[0];
    }
    int findMinArrowShots(vector<vector<int>>& points) {
        sort(points.begin(), points.end(), cmp);
        int res = 0;
        int cur = -0x3f3f3f3f;
        for (int i = 0; i < points.size(); i ++ ) {
            if (i == 0 || cur < points[i][0]) {
                res ++ ;
                cur = points[i][1];
            }
        }
        return res;
    }
};
```
