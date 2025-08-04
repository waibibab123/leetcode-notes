# 75、颜色分类
题目难度：mid

题目网址：https://leetcode.cn/problems/sort-colors/

代码语言：cpp
## 题解
### 方法一、三指针
遍历数组，并额外设置两个指针 zero 和 two 分别指向数组起始和末尾，遍历数组，遇到 2 就与 two 指向元素交换并将 two 指针前移，遇到 0 就与 zero 指向元素交换并将 zero 指针后移，以此实现数组的排序

**代码**

C++

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int zero = 0, two = nums.size() - 1;
        for (int i = 0; i <= two; i ++ ) {
            while (nums[i] == 2 && i <= two) swap(nums[i], nums[two -- ]);
            if (nums[i] == 0) swap(nums[i], nums[zero ++ ]);
        }
    }
};
```
