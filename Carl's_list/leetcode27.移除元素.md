# 27、移除元素

题目网址：https://leetcode.cn/problems/remove-element/description/

题目难度：easy

代码语言：cpp
## 题解
### 方法一、双指针
设置快慢指针，快指针fast每次往前移动一格，当fast指向的元素不等于需要移除的元素时，才让慢指针往前移动

**代码**

C++

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow = 0, fast = 0;
        for (; fast < nums.size(); fast ++ ) {
            if (nums[fast] != val) nums[slow ++ ] = nums[fast];
        }
        return slow;
    }
};
```
