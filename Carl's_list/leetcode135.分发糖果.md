# 135、分发糖果
贪心

维护一个记录每个人需要糖果的数组cnt，初始化全1，从第二个往后遍历，每个和左边的人比较，若评分高于左边的人，`cnt[i] = cnt[i - 1] + 1`，从而更新1~cnt.size()-1的所有人，然后从倒数第二个往前遍历，每个和右边比较，若评分高于右边的人
就`cnt[i] = cnt[i + 1] + 1`，从而更新0~cnt.size()-2的所有人，此时除了两边的人更新了一次之外，其它人都被更新了两次，并满足每个人分得的糖果数一定高于两边那个评分低于这个人的糖果数

C++
```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> cnt(ratings.size(), 1);
        for (int i = 1; i < ratings.size(); i ++ ) {
            if (ratings[i] > ratings[i - 1]) cnt[i] = cnt[i - 1] + 1;
        }
        for (int i = ratings.size() - 2; i >= 0; i -- ) {
            if (ratings[i] > ratings[i + 1]) cnt[i] = max(cnt[i + 1] + 1, cnt[i]);
        }
        int res = 0;
        for (int i = 0; i < cnt.size(); i ++ ) res += cnt[i];
        return res;
    }
};
```
