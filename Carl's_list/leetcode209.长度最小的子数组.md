# 209、长度最小的子数组
题目网址：https://leetcode.cn/problems/minimum-size-subarray-sum/description/

题目难度：mid

代码语言：cpp

## 题解
### 方法一、滑动窗口
我们维护一个滑动窗口，l、r分别表示其左右端点，遍历nums时，每次让r往右扩展一个元素，如果滑动窗口中的元素之和大于等于target，就让l不断往右以缩减窗口大小，直到元素之和小于target。每次缩减窗口时我们记录当前满足总和大于等于target的长度最小值，遍历完nums
之后，这个最小值就是全局的最小值。

**代码**

C++

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int res = 0x3f3f3f3f;
        int sum = 0;
        int l = 0, r = 0;
        for (; r < nums.size(); r ++ ) {
            sum += nums[r];
            while (l <= r && sum >= target) {
                res = min(res, r - l + 1);
                sum -= nums[l ++ ];
            }
        }
        return res == 0x3f3f3f3f ? 0 : res;
    }
};
```
