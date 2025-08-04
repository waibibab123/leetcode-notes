# 112、路径总和
题目网址：https://leetcode.cn/problems/path-sum/description/

题目难度：easy

代码语言：cpp
## 题解
此题与leetcode257较为相似，依旧采用前序遍历法解决，

中：如果当前的节点是叶子结点，如果目标值恰好等于节点值就返回true，否则返回false

左、右：依次递归到左节点和右节点，递归函数中的参数“目标值”需要修改为原来的目标值减去当前的叶子结点的值

只要左右子树递归中有一个返回true，则最终返回true

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
    bool traverse(TreeNode* root, int targetSum) {
        if (root->left == NULL && root->right == NULL) {
            if (root->val == targetSum) return true;
            else return false;
        } 
        bool left = false, right = false;
        if (root->left) {
            left = traverse(root->left, targetSum - root->val);
        }
        if (root->right) {
            right = traverse(root->right, targetSum - root->val);
        }
        return left || right;
    }
    bool hasPathSum(TreeNode* root, int targetSum) {
        if (root == NULL) return false;
        return traverse(root, targetSum);
    }
};
```
