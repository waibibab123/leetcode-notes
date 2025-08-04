# 108、将有序数组转换为二叉搜索树
题目网址：https://leetcode.cn/submissions/detail/640743676/

题目难度：easy

代码语言：cpp
## 题解
使用前序遍历，首先创造根节点root，值就是数组中间那个元素，随后分别将数组左半部分（不含中间那个元素）和数组右半部分（不含中间那个元素）作为参数传入递归函数，返回值依次赋值给root的左右子树。

C++
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
private:
    TreeNode* traverse(vector<int>& nums, int left, int right) {
        if (left > right) return NULL;
        TreeNode* root = new TreeNode(nums[(left + right) / 2]);
        root->left = traverse(nums, left, (left + right) / 2 - 1);
        root->right = traverse(nums, (left + right) / 2 + 1, right);
        return root;
    }
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return traverse(nums, 0, nums.size() - 1);
    }
};
```
