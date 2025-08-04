# 110、平衡二叉树
题目网址：https://leetcode.cn/problems/balanced-binary-tree/submissions/595261036/

题目难度：easy

代码语言：cpp
## 题解
本题采用前序遍历，首先判断根节点的左右子树的深度差的绝对值是否大于一，若是一直接返回false，然后依次递归到左右子树，当返回值均为true时，最终就返回true

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
    int getDepth(TreeNode* root) {
        if (root == NULL) return 0;
        int left = getDepth(root->left);
        int right = getDepth(root->right);
        return max(left, right) + 1;
    }
    bool isBalanced(TreeNode* root) {
        if (root == NULL) return true;
        if (abs(getDepth(root->left) - getDepth(root->right)) > 1) return false;
        return isBalanced(root->left) && isBalanced(root->right);
    }
};
```
