# 530、二叉搜索树的最小绝对值差
题目网址：https://leetcode.cn/problems/minimum-absolute-difference-in-bst/description/

题目难度：easy

代码语言：cpp
## 题解
在[leetcode98、验证二叉搜索树的“直接递归方法”](./leetcode98.验证二叉搜索树)的基础上，添加一个全局变量res，用于记录在遍历过程中两个节点之间的最小绝对值差

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
    int res = INT_MAX;
    TreeNode* pre = NULL;
    void traverse(TreeNode* root) {
        if (root == NULL) return;
        traverse(root->left);
        if (pre == NULL) pre = root;
        else {
            res = min(res, abs(pre->val - root->val));
            pre = root;
        }
        traverse(root->right);
    }
    int getMinimumDifference(TreeNode* root) {
        traverse(root);
        return res;
    }
};
```
