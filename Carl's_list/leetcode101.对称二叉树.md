# 101、对称二叉树
题目网址：https://leetcode.cn/problems/symmetric-tree/description/

题目难度：easy

代码语言：cpp
## 题解
step1.确定参数：编写一个遍历函数，传入根节点的左右节点

step2.边界处理：
* 如果左右结点均空，返回true
* 如果只有一个为空，返回false

step3.确定单次遍历逻辑：
在处理边界之后，左右结点均为非空，首先判断左右节点的值是否相同，若不同，直接返回false，否则继续进行，判断两个条件：
* 1.左节点的左节点和右节点的右节点是否相同？记为flag1
* 2.左节点的右节点和右节点的左节点是否相同？记为flag2

如果1和2同时满足，那么最终返回true

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
    bool traverse(TreeNode* node1, TreeNode* node2) {
        if (node1 == NULL && node2 == NULL) return true;
        if (node1 == NULL && node2 != NULL) return false;
        if (node1 != NULL && node2 == NULL) return false;
        if (node1->val != node2->val) return false;
        bool flag1 = traverse(node1->left, node2->right);
        bool flag2 = traverse(node1->right, node2->left);
        return flag1 && flag2;
    }
    bool isSymmetric(TreeNode* root) {
        if (root == NULL) return true;
        return traverse(root->left, root->right);
    }
};
```
