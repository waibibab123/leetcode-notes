# 669、修剪二叉搜索树
题目网址：https://leetcode.cn/problems/trim-a-binary-search-tree/description/

题目难度：mid

代码语言：cpp
## 题解
前序遍历，对于根结点，如果其值大于high，直接返回root->left，如果其值小于low，直接返回root->right

左：直接让根节点的左子树调用本函数

右：直接让根节点的右子树调用本函数

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
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        if (root == NULL) return NULL;
        if (root->val < low) return trimBST(root->right, low, high);
        if (root->val > high) return trimBST(root->left, low, high);
        root->left = trimBST(root->left, low, high);
        root->right = trimBST(root->right, low, high);
        return root;
    }
};
```
