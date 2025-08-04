# 53、最大子数组和
贪心，维护两个变量res和count，前者用来记录最终答案，后者用来记录部分和，然后遍历数组，每次遍历首先让遍历到的元素添加到count中，如果然后更新res（取res和count最大值），最后判断
count是否小于0，如果小于零，就将count重新设置为0，因为小于0的数与后面的数相加必然会**更小**，因此就放弃前面这个暂时的部分和。

C++
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = INT_MIN;
        int count = 0;
        for (int i = 0; i < nums.size(); i ++ ) {
            count += nums[i];
            res = max(res, count);
            if (count < 0) count = 0;
        }
        return res;
    }
};
```
