# 222、完全二叉树的节点个数
easy

C++
## 题解
这题需要利用完全二叉树的性质：

首先计算左右子树的深度：
* 若左右子树深度一致，那么左子树为满，结点个数就是1<<leftLevel - 1
* 若不一致，那么右子树为满，结点个数就是1<<rightLevel - 1
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
    //统计树的深度，仅限于对完全二叉树这样统计
    int getLevels(TreeNode* root) {
        if (root == NULL) return 0;
        int level = 0;
        while (root) {
            level ++ ;
            root = root->left;
        }
        return level;
    }
    int countNodes(TreeNode* root) {
        if (root == NULL) return 0;
        int leftLevels = getLevels(root->left);
        int rightLevels = getLevels(root->right);
        if (leftLevels == rightLevels) {
            return countNodes(root->right) + (1 << leftLevels);
        }
        else return countNodes(root->left) + (1 << rightLevels);
    }
};
```
