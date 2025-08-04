# 236.二叉树的最近公共祖先
题目网址：https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/description/

题目难度：mid

代码语言：cpp
## 题解
本题的方法是后续遍历，首先考虑边界情况：
* 如果root为NULL，则直接返回NULL
* 如果root == p，直接返回p，如果root == q，直接返回q，这是基于下面两个原因：
  * 节点自身可作为公共祖先。当p或者q中的某一个节点本身就是另一个节点的祖先时，这个节点就是它们的最近公共祖先。
  * 递归回溯的需要。当碰到 p 或者 q 时就返回该节点，这样可以保证将节点的存在信息向上传递。
然后就是确定单次递归逻辑：
* 左、右：直接传入左右子树以调用函数进行递归，分别返回left和right
* 中：如果left和right都不为空，那么返回root，如果left为空，则返回right；如果right为空，则返回left；如果都为空，则返回NULL

C++
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL) return NULL;
        if (root == p) return p;
        if (root == q) return q;
        auto left = lowestCommonAncestor(root->left, p, q);
        auto right = lowestCommonAncestor(root->right, p, q);
        if (left != NULL && right != NULL) return root;
        return left ? left : right;
    }
};
```
