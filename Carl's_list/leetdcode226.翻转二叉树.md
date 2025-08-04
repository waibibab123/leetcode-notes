# 226、翻转二叉树
题目网址：https://leetcode.cn/problems/invert-binary-tree/description/

题目难度：easy

代码语言：cpp
## 题解
可以使用前序遍历进行递归解决

前序遍历：中-左-右

中：swap(root->left, root->right)

左、右：dfs(root->left); dfs(root->right)

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
    void traverse(TreeNode* root) {
        if (root == NULL) return;
        swap(root->left, root->right);
        traverse(root->left);
        traverse(root->right);
    }
    TreeNode* invertTree(TreeNode* root) {
        traverse(root);
        return root;
    }
};
```
