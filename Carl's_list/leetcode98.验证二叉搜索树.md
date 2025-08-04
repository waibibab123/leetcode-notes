# 98、验证二叉搜索树
题目网址：https://leetcode.cn/problems/validate-binary-search-tree/submissions/638809141/

题目难度：mid

代码语言：cpp
## 题解
### 方法一、
一种简单的思路是先对这个二叉树进行中序遍历，然后检验中序遍历序列是不是严格单调递增的，如果是，那么就是二叉搜索树，代码省略
### 方法二、
直接遍历法，也就是一边进行中序遍历，另一边判断遍历的节点值是不是有序的

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
    TreeNode* pre = NULL;
    bool isValidBST(TreeNode* root) {
        if (root == NULL) return true;
        if (isValidBST(root->left) == false) return false;
        if (pre == NULL) pre = root;
        else {
            if (pre->val >= root->val) return false;
            pre = root;
        }
        if (isValidBST(root->right) == false) return false;
        return true;
    }
};
```
