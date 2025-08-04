# 152、乘积最大子数组
难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/maximum-product-subarray/description/

## 题解
### 方法一、动态规划
**思路来源**：[力扣-灵茶山艾府](https://leetcode.cn/problems/maximum-product-subarray/solutions/2968916/dong-tai-gui-hua-jian-ji-gao-xiao-python-i778/?envType=study-plan-v2&envId=top-100-liked)

step1.状态表示：我们将`dp_max[i]`表示为右端点下标为i的子数组的最大乘积，`dp_min[i]`表示为右端点下标为i的子数组的最小乘积

step2.状态转移：

* 如果nums[i]单独组成一个子数组，那么`dp_max[i] = nums[i]`
* nums[i]和前面的子数组拼起来，也就是在右端点下标为i-1的乘积最大子数组之后添加nums[i]，那么`dp_max[i] = dp_max[i - 1] * nums[i]`，也可以在右端点下标为i-1的乘积最小子数组之后添加nums[i]，那么`dp_max[i] = dp_min[i - 1] * nums[i]`，把这两种都算一下的好处是无需判断nums[i]的正负

因此在每次循环时，只需取三者最大值:`max(nums[i], dp_max[i - 1] * nums[i], dp_min[i - 1] * nums[i])`，如何更新dp_min？ 只需：`dp_min[i] = min(nums[i], dp_max[i - 1] * nums[i], dp_min[i - 1] * nums[i])`

step3.边界处理：由于以nums[0]为右端点的子数组乘积只能是nums[0]，因此初始值:`dp_max[0] = dp_min[0] = nums[0]`

## 代码
C++

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        vector<int> dp_max(nums.size(), -0x3f3f3f3f);
        vector<int> dp_min(nums.size(), 0x3f3f3f3f);
        dp_max[0] = dp_min[0] = nums[0];
        for (int i = 1; i < nums.size(); i ++ ) {
            int x = nums[i];
            dp_max[i] = max({x, dp_max[i - 1] * x, dp_min[i - 1] * x});
            dp_min[i] = min({x, dp_max[i - 1] * x, dp_min[i - 1] * x});
        }
        int res = -0x3f3f3f3f;
        for (int i = 0; i < dp_max.size(); i ++ ) res = max(res, dp_max[i]);
        return res;
    }
};
```
