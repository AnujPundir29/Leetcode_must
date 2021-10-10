### [572\. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)

Difficulty: **Easy**  

Related Topics: [Tree](https://leetcode.com/tag/tree/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [String Matching](https://leetcode.com/tag/string-matching/), [Binary Tree](https://leetcode.com/tag/binary-tree/), [Hash Function](https://leetcode.com/tag/hash-function/)


Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)

```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
```

**Constraints:**

*   The number of nodes in the `root` tree is in the range `[1, 2000]`.
*   The number of nodes in the `subRoot` tree is in the range `[1, 1000]`.
*   `-10<sup>4</sup> <= root.val <= 10<sup>4</sup>`
*   `-10<sup>4</sup> <= subRoot.val <= 10<sup>4</sup>`


#### Solution

Language: **C++**

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool helper(TreeNode* r1,TreeNode* r2)
    {
        if(!r1 and !r2)  return 1;
        
        if(!r1 or !r2)  return 0;
        
        return r1->val==r2->val and helper(r1->left,r2->left) and helper(r1->right,r2->right);
    }
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(!root and !subRoot)  return 1;
        
        if(root)
            return helper(root,subRoot) or isSubtree(root->left,subRoot) or isSubtree(root->right,subRoot);
        return false;
    }
    
    // Another gfg soln
    
    vector<TreeNode*> nodes;
public:
    bool isSubtree(TreeNode* S, TreeNode* T) {
        if (!S && !T) return true;
        if (!S || !T) return false;
        getDepth(S, getDepth(T, -1));
        for (TreeNode* n: nodes)
            if (identical(n, T))
                return true;
        return false;
    }
    int getDepth(TreeNode* r, int d) {
        if (!r)
            return -1;
        int depth = max(getDepth(r->left, d), getDepth(r->right, d)) + 1;
        // Check if depth equals required value
        // Require depth is -1 for tree t (only return the depth, no push)
        if (depth == d)
            nodes.push_back(r);
        return depth;
    }
    bool identical(TreeNode* a, TreeNode* b) {
        if (!a && !b) return true;
        if (!a || !b || a->val != b->val) return false;
        return identical(a->left, b->left) && identical(a->right, b->right);
    }
};
```
