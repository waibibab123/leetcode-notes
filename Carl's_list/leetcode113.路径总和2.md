# 113、路径总和2
题目网址：https://leetcode.cn/problems/path-sum-ii/description/

题目难度：mid

代码语言：cpp
## 题解
这道题目和[leetcode112.路径总和](./leetcode112.路径总和.md)是类似的，唯一的区别是加了一个答案数组和路径数组，然后记得在每次递归之后恢复结果即可

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
    vector<vector<int>> res;
    vector<int> path;
    void traverse(TreeNode* root, int targetSum) {
        path.push_back(root->val);
        if (root->left == NULL && root->right == NULL) {
            if (root->val == targetSum) {
                res.push_back(path);
            }
            return;
        }
        if (root->left) {
            traverse(root->left, targetSum - root->val);
            path.pop_back();
        }
        if (root->right) {
            traverse(root->right, targetSum - root->val);
            path.pop_back();
        }
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        if (root == NULL) return res;
        traverse(root, targetSum);
        return res;
    }
};
```
