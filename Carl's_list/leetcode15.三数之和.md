# 15、三数之和
题目网站：https://leetcode.cn/problems/3sum/description/

题目难度：mid

代码语言：cpp
## 题解
### 方法一、双指针
大致思路：首先对数组排序，接着，使用三个指针，第一个指针k作为第一层遍历，每次遍历时，再分别使用两个指针l=k+1，和r（指向数组末尾），分三种情况：三指针指向元素和为0，则加入答案，并l++和r--，大于0，则r--，小于0，则l++

剪枝优化（去重）：
对于k，如果指向的元素大于0直接结束（break）；如果新的k与上一个k指向元素相同，continue
对于l和r，每次记录答案后，如果下一个（右边的）l指向元素等于当前l指向元素，则l++，如果下一个（左边的）r指向元素等于当前r指向元素，则r--

C++

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        for (int k = 0; k < nums.size(); k ++ ) {
            if (k > 0 && nums[k] == nums[k - 1]) continue;
            int left = k + 1;
            int right = nums.size() - 1;
            while (left < right) {
                if (nums[k] + nums[left] + nums[right] > 0) right -- ;
                else if (nums[k] + nums[left] + nums[right] < 0) left ++ ;
                else {
                    res.push_back(vector<int>{nums[k], nums[left], nums[right]});
                    while (left < right && nums[left + 1] == nums[left]) left ++ ;
                    while (left < right && nums[right - 1] == nums[right]) right -- ;
                    left ++ ;
                    right -- ;
                }
            }
        }
        return res;
    }
};
```
