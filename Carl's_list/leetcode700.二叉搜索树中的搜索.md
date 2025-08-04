# 700、二叉搜索数中的搜索
题目网址：https://leetcode.cn/problems/search-in-a-binary-search-tree/description/

题目难度：easy

代码语言：cpp
## 题解
直接进行前序遍历即可，如果当前遍历到的节点值等于val，直接返回，若大于，则遍历左孩子，若小于，则遍历右孩子

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
    TreeNode* searchBST(TreeNode* root, int val) {
        if (root == NULL) return NULL;
        if (root->val == val) return root;
        else if (root->val < val) return searchBST(root->right, val);
        else return searchBST(root->left, val);
    }
};
```
