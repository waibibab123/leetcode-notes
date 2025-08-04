# 136、只出现一次的数字
题目难度：easy

题目网址：https://leetcode.cn/problems/single-number/description/

代码语言：cpp
## 题解
### 方法一、位运算
由于任何两个相同的数异或的值必然为0，而且这个数组恰好除了只出现一次的数字之外，其它数字都出现了两次，因此我们把数组所有元素依次作异或，那么最终的值就是只出现了一次的数字

**代码**

C++

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        for (int i = 1; i < nums.size(); i ++ ) nums[0] ^= nums[i];
        return nums[0];
    }
};
```
