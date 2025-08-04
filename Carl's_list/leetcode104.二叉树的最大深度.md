# 104、二叉树的最大深度
题目网址：https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/

题目难度：easy

代码语言：cpp
## 题解
如果root是空，直接返回深度为零，反之，因此求得左孩子和右孩子的深度：`maxDepth(root->left)、maxDepth(root->right)`，取最大值加一即为整个数的最大深度

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
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL) return 0;
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        return max(left, right) + 1;
    }
};
```
