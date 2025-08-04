# 106、从中序与后序遍历序列构造二叉树
题目网址：https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/submissions/607659763/

题目难度：mid

代码语言：cpp
## 题解
边界情况：如果两个数组为空，那么直接返回NULL；如果数组只有一个元素，直接返回一个结点root即可

一般情况下，我们首先获取到后序遍历序列的最后一个值val，这个值必然为最终生成二叉树的根节点的值，随后我们遍历中序序列，找到中序遍历序列中值与val相同的元素下标，这个下标便可以把中序遍历序列分为左右两个部分，左边就是最终生成二叉树的左子树的
中序遍历序列，右边就是最终生成二叉树的中序遍历序列，但是如何得到最终生成二叉树的左右子树的后序遍历序列呢？其实很简单，对于同一个二叉树，中序遍历序列和后续遍历序列一定是相同的，因此可以利用这个性质再构建出最终生成二叉树的左右子树的后序遍历序列
有了上述四个序列之后，我们就可以通过递归依次得到根节点root的左右子树

**代码**

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
private:
    TreeNode* traversal (vector<int>& inorder, vector<int>& postorder) {
        if (postorder.size() == 0) return NULL;

        // 后序遍历数组最后一个元素，就是当前的中间节点
        int rootValue = postorder[postorder.size() - 1];
        TreeNode* root = new TreeNode(rootValue);

        // 叶子节点
        if (postorder.size() == 1) return root;

        // 找到中序遍历的切割点
        int delimiterIndex;
        for (delimiterIndex = 0; delimiterIndex < inorder.size(); delimiterIndex++) {
            if (inorder[delimiterIndex] == rootValue) break;
        }

        // 切割中序数组
        // 左闭右开区间：[0, delimiterIndex)
        vector<int> leftInorder(inorder.begin(), inorder.begin() + delimiterIndex);
        // [delimiterIndex + 1, end)
        vector<int> rightInorder(inorder.begin() + delimiterIndex + 1, inorder.end() );

        // postorder 舍弃末尾元素
        postorder.resize(postorder.size() - 1);

        // 切割后序数组
        // 依然左闭右开，注意这里使用了左中序数组大小作为切割点
        // [0, leftInorder.size)
        vector<int> leftPostorder(postorder.begin(), postorder.begin() + leftInorder.size());
        // [leftInorder.size(), end)
        vector<int> rightPostorder(postorder.begin() + leftInorder.size(), postorder.end());

        root->left = traversal(leftInorder, leftPostorder);
        root->right = traversal(rightInorder, rightPostorder);

        return root;
    }
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if (inorder.size() == 0 || postorder.size() == 0) return NULL;
        return traversal(inorder, postorder);
    }
};
```
