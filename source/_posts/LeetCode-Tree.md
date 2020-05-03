---
title: LeetCode-Tree
categories: [算法]
tags: [算法,C++,数据结构]
copyright: true
comments: true
top: false
author: XQ
mathjax: false
date: 2019-02-01 20:56:54
updated: 2019-02-12 20:56:54
keywords:
description: LeetCode树专题。
passwords:
img:

---

``` cpp
给定一个二叉树，返回它的中序 遍历。

示例:

输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
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
    
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        if(root->left)  res = inorderTraversal(root->left);
        res.push_back(root->val);
        if(root->right) {
            vector<int> right = inorderTraversal(root->right);
            for(auto i = 0; i < right.size(); i++){
                res.push_back(right[i]);
            }
        }
        return res;
    }
};
```

``` cpp
给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。
示例 1:

输入:
    2
   / \
  1   3
输出: true
示例 2:

输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
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
    bool isValidBST(TreeNode* root) {
        if(!root) return true;
        bool left;
        if(root->left){
            left = isValidBST(root->left);
        }
        bool right;
        if(root->right){
            right = isValidBST(root->right);
        }
        if(root->left && root->right){
            if(left && right && root->val > findBSTMax(root->left) && root->val < findBSTMin(root->right)) return true;
            else return false;
        }
        else if(!root->left && root->right){
            if(right && root->val < findBSTMin(root->right)) return true;
            else return false;
        }
        else if(root->left && !root->right){
            if(left && root->val > findBSTMax(root->left)) return true;
            else return false;
        }
        else return true;
    }
    int findBSTMax(TreeNode* root){
        if(!root->right) return root->val;
        return findBSTMax(root->right);
        
        
    }
    int findBSTMin(TreeNode* root){
        if(!root->left) return root->val;
        return findBSTMax(root->left);
    }
};


```

``` cpp
给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

示例 1:

输入:       1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

输出: true
示例 2:

输入:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]

输出: false
示例 3:

输入:       1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

输出: false
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
    
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(q == NULL && p == NULL) return true;
        if(q != NULL && p!= NULL){
            if(q->val != p->val) return false;
            else return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
        } else return false;
        
        
    }
};
```

``` cpp
给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
public:
    bool isSymmetric(TreeNode* pRoot)
    {
        return isSymmetric(pRoot,pRoot);
    }
    bool isSymmetric(TreeNode* pleft,TreeNode* pright)
    {
        if(pleft==NULL&&pright==NULL)
            return true;
        if(pleft==NULL||pright==NULL)
            return false;
        if(pleft->val!=pright->val)
            return false;
        return isSymmetric(pleft->left,pright->right)&&isSymmetric(pleft->right,pright->left);
    }
};



```

``` cpp
给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]


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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        queue<TreeNode*> q;
        if(!root) return res;
        q.push(root);
        int last = 1;
        
        while(!q.empty()){
            vector<int> temp;
            int k = 0;
            for(int i = 0; i < last; i ++){
                
                temp.push_back(q.front()->val);
                if(q.front()->left) {
                    q.push(q.front()->left);
                    k ++;
                }
                if(q.front()->right) {
                    q.push(q.front()->right);
                    k++;
                }
                q.pop();
 
            }
            last = k;
            res.push_back(temp);
        }
        return res;
    }
};

```

``` cpp
给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回锯齿形层次遍历如下：

[
  [3],
  [20,9],
  [15,7]
]
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        deque<TreeNode*> q;
        if(!root) return res;
        q.push_back(root);
        int last = 1;
        int layer = 2;
        while(!q.empty()){
            vector<int> temp;
            int k = 0;
            
            for(int i = 0; i < last; i ++){ 
                
                if(layer%2 == 0){
                    temp.push_back(q.front()->val);
                    
                    if(q.front()->left) {
                        q.push_back(q.front()->left);
                        k ++;
                    }
                    if(q.front()->right) {
                        q.push_back(q.front()->right);
                        k ++;
                    }
                    q.pop_front();
                }
                else{
                    temp.push_back(q.back()->val);
                    if(q.back()->right){
                        q.push_front(q.back()->right);
                        k++;
                    }
                    if(q.back()->left){
                        q.push_front(q.back()->left);
                        k++;
                    }
                    q.pop_back();
                    
                    
                }
                

            }
            
            last = k;
            layer ++;
            res.push_back(temp);
        }
        return res;
    }
};

```
执行用时: 4 ms, 在Binary Tree Zigzag Level Order Traversal的C++提交中击败了99.45% 的用户

``` cpp
给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其自底向上的层次遍历为：

[
  [15,7],
  [9,20],
  [3]
]
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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        
        vector<vector<int>> res;
        queue<TreeNode*> q;
        if(!root) return res;
        q.push(root);
        int last = 1;
        stack<vector<int>> s;
        while(!q.empty()){
            vector<int> temp;
            int k = 0;
            for(int i = 0; i < last; i ++){
                
                temp.push_back(q.front()->val);
                if(q.front()->left) {
                    q.push(q.front()->left);
                    k ++;
                }
                if(q.front()->right) {
                    q.push(q.front()->right);
                    k++;
                }
                q.pop();
 
            }
            
            last = k;
            s.push(temp);
        }
        while(!s.empty()){
            res.push_back(s.top());
            s.pop();
     
        }

        return res;
    }
};

```
执行用时: 4 ms, 在Binary Tree Level Order Traversal II的C++提交中击败了100.00% 的用户

``` cpp
给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？

示例:

输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
class Solution {
public:
    int numTrees(int n) {
        vector<int>dp(n+1,0); 
        dp[0]=1; dp[1]=1; 
        for(int i = 2; i<=n ;i++) 
            for(int j = 0 ; j < i ; j++) 
                dp[i] += dp[j] * dp[i - j - 1]; 
        return dp[n];
    }
     
};
```
执行用时: 0 ms, 在Unique Binary Search Trees的C++提交中击败了100.00% 的用户

``` cpp
给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

示例:

给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回它的最小深度  2.
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
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        int depth_left = 0;
        int depth_right = 0;
        if(root->left){
            depth_left = minDepth(root->left);
        }
        if(root->right){
            depth_right = minDepth(root->right);
        }
        if(!root->left){
            return ++depth_right;
        }
        if(!root->right){
            return ++depth_left;
        }
        return ++(depth_left > depth_right? depth_right : depth_left);
    }
};
```
执行用时: 4 ms, 在Minimum Depth of Binary Tree的C++提交中击败了100.00% 的用户

``` cpp
给定一个二叉树，原地将它展开为链表。

例如，给定二叉树

    1
   / \
  2   5
 / \   \
3   4   6
将其展开为：

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6


/**/


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
    void flatten(TreeNode* root) {
        if(!root) return;
        if(root->left)flatten(root->left);
        if(root->right)flatten(root->right);
        TreeNode * matchNode = findMatchNode(root->left);
        if(matchNode) {
            matchNode->right = root->right;
            root->right = root->left;
            root->left = NULL;//没有置空这一步会出问题
        }
    }
    TreeNode * findMatchNode(TreeNode * root){
        if(!root) return NULL;
        if(!root->right) return root;
        return findMatchNode(root->right);
    }
};
```

``` cpp 
给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

说明: 叶子节点是指没有子节点的节点。

示例: 
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2。

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
    bool hasPathSum(TreeNode* root, int sum) {
 
        if(!root) return false;

        if(!root->left && !root->right) {
            return sum - root->val == 0 ? true : false;
        }
        else {
            return hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val);
        }
        
    }
};
```
执行用时: 12 ms, 在Path Sum的C++提交中击败了26.91% 的用户

更优的解法还没搞明白，研究一下
``` cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
static auto x = []() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    return 0;
}();
class Solution {
public:
    vector<int> path_sum(TreeNode *root)
    {
        vector<int> ret;
        if(root == NULL)
            return ret;
        vector<int> t1 = path_sum(root -> left);
        vector<int> t2 = path_sum(root -> right);
        for(int i = 0; i < t1.size(); i++)
            ret.push_back(t1[i] + root -> val);
        for(int i = 0; i < t2.size(); i++)
            ret.push_back(t2[i] + root -> val);
        if(ret.empty())
            ret.push_back(root -> val);
        return ret;
    }
    bool hasPathSum(TreeNode* root, int sum) {
        if(root == NULL)
            return false;
        vector<int> t = path_sum(root);
        for(int i = 0; i < t.size(); i++)
        {
            if(t[i] == sum)
                return true;
        }
        return false;
    }
};
```

``` cpp
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5

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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return sortedArrayToBST(nums, 0, nums.size()-1);
    }

    TreeNode* sortedArrayToBST(vector<int>& nums, int a, int b){
        if(a > b) return NULL;
        if(a == b) {
            return new TreeNode(nums[a]);
        }
        int mid = (a+b)/2;
        TreeNode * root = new TreeNode(nums[mid]);
        root->left = sortedArrayToBST(nums, a, mid-1);
        root->right = sortedArrayToBST(nums, mid+1, b);
        return root;

    }
};
//执行用时: 12 ms, 在Convert Sorted Array to Binary Search Tree的C++提交中击败了97.69% 的用户
```


``` cpp

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

示例 1:

给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。


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
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        if(abs(height(root->left) - height(root->right)) <= 1){
            if(isBalanced(root->left)&&isBalanced(root->right)) return true;
            else return false;
        }
        return false;
    }
    int height(TreeNode * root){
        if(!root) return 0;
        return max(height(root->left),height(root->right))+1;

    }
};
//执行用时: 8 ms, 在Balanced Binary Tree的C++提交中击败了98.12% 的用户
```


``` cpp
给定一个二叉树，返回它的 前序 遍历。

 示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
进阶: 递归算法很简单，你可以通过迭代算法完成吗？

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
    vector<int> preorderTraversal(TreeNode* root) {
        
        vector<int> res;
        if(!root) return res;
        res.push_back(root->val);
        if(root->left) {
            vector<int> left = preorderTraversal(root->left);
            for(int i = 0; i < left.size(); i++){
                res.push_back(left[i]);
            }
        }
        if(root->right) {
            vector<int> right = preorderTraversal(root->right);
            for(int i = 0; i < right.size(); i++){
                res.push_back(right[i]);
            }
        }
        return res;
    }
    
};
//执行用时: 0 ms, 在Binary Tree Preorder Traversal的C++提交中击败了100.00% 的用户
```


``` cpp
给定一个非空二叉树, 返回一个由每层节点平均值组成的数组.

示例 1:

输入:
    3
   / \
  9  20
    /  \
   15   7
输出: [3, 14.5, 11]
解释:
第0层的平均值是 3,  第1层是 14.5, 第2层是 11. 因此返回 [3, 14.5, 11].

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
    vector<double> averageOfLevels(TreeNode* root) {
        vector<double> res;
        queue<TreeNode*> q;
        if(!root) return res;
        q.push(root);
        int last = 1;
        
        while(!q.empty()){
            vector<int> temp;
            int k = 0;
            for(int i = 0; i < last; i ++){
                
                temp.push_back(q.front()->val);
                if(q.front()->left) {
                    q.push(q.front()->left);
                    k ++;
                }
                if(q.front()->right) {
                    q.push(q.front()->right);
                    k++;
                }
                q.pop();
 
            }
            last = k;
            long sum = 0;
            for(int i = 0; i < temp.size(); i++){
                sum += temp[i];
            }
            res.push_back((double)sum/temp.size());
        }
        return res;
    }
};
//执行用时: 20 ms, 在Average of Levels in Binary Tree的C++提交中击败了25.57% 的用户
```


``` cpp
/*
 * @lc app=leetcode.cn id=226 lang=cpp
 *
 * [226] 翻转二叉树
 *
 * https://leetcode-cn.com/problems/invert-binary-tree/description/
 *
 * algorithms
 * Easy (65.87%)
 * Total Accepted:    9.4K
 * Total Submissions: 14.3K
 * Testcase Example:  '[4,2,7,1,3,6,9]'
 *
 * 翻转一棵二叉树。
 * 
 * 示例：
 * 
 * 输入：
 * 
 * ⁠    4
 * ⁠  /   \
 * ⁠ 2     7
 * ⁠/ \   / \
 * 1   3 6   9
 * 
 * 输出：
 * 
 * ⁠    4
 * ⁠  /   \
 * ⁠ 7     2
 * ⁠/ \   / \
 * 9   6 3   1
 * 
 * 备注:
 * 这个问题是受到 Max Howell 的 原问题 启发的 ：
 * 
 * 谷歌：我们90％的工程师使用您编写的软件(Homebrew)，但是您却无法在面试时在白板上写出翻转二叉树这道题，这太糟糕了。
 * 
 */
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
    TreeNode* invertTree(TreeNode* root) {
        if (!root)
            return NULL;
        TreeNode *left = NULL;
        TreeNode *right = NULL;
        if (root->left)
            left = invertTree(root->left);
        if (root->right)
            right = invertTree(root->right);

        root->left = right;
        root->right = left;
        return root;
    }
};
//执行用时: 0 ms, 在Invert Binary Tree的C++提交中击败了100.00% 的用户
```

``` cpp
/*
 * @lc app=leetcode.cn id=669 lang=cpp
 *
 * [669] 修剪二叉搜索树
 *
 * https://leetcode-cn.com/problems/trim-a-binary-search-tree/description/
 *
 * algorithms
 * Easy (57.78%)
 * Total Accepted:    2.5K
 * Total Submissions: 4.3K
 * Testcase Example:  '[1,0,2]\n1\n2'
 *
 * 给定一个二叉搜索树，同时给定最小边界L 和最大边界 R。通过修剪二叉搜索树，使得所有节点的值在[L, R]中 (R>=L)
 * 。你可能需要改变树的根节点，所以结果应当返回修剪好的二叉搜索树的新的根节点。
 * 
 * 示例 1:
 * 
 * 
 * 输入: 
 * ⁠   1
 * ⁠  / \
 * ⁠ 0   2
 * 
 * ⁠ L = 1
 * ⁠ R = 2
 * 
 * 输出: 
 * ⁠   1
 * ⁠     \
 * ⁠      2
 * 
 * 
 * 示例 2:
 * 
 * 
 * 输入: 
 * ⁠   3
 * ⁠  / \
 * ⁠ 0   4
 * ⁠  \
 * ⁠   2
 * ⁠  /
 * ⁠ 1
 * 
 * ⁠ L = 1
 * ⁠ R = 3
 * 
 * 输出: 
 * ⁠     3
 * ⁠    / 
 * ⁠  2   
 * ⁠ /
 * ⁠1
 * 
 * 
 */
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
    TreeNode* trimBST(TreeNode* root, int L, int R) {
        if (!root)
            return NULL;
        if (root->val < L)
        {
            return trimBST(root->right, L, R);
        }
        else if (root->val > R)
        {
            return trimBST(root->left, L, R);
        }
        else
        {
            root->left = trimBST(root->left, L, R);
            root->right = trimBST(root->right, L, R);
            return root;
        }
    }
};
//执行用时: 12 ms, 在Trim a Binary Search Tree的C++提交中击败了97.21% 的用户
```

``` cpp
/*
 * @lc app=leetcode.cn id=657 lang=cpp
 *
 * [657] 机器人能否返回原点
 *
 * https://leetcode-cn.com/problems/robot-return-to-origin/description/
 *
 * algorithms
 * Easy (67.40%)
 * Total Accepted:    10.9K
 * Total Submissions: 16.2K
 * Testcase Example:  '"UD"'
 *
 * 在二维平面上，有一个机器人从原点 (0, 0) 开始。给出它的移动顺序，判断这个机器人在完成移动后是否在 (0, 0) 处结束。
 * 
 * 移动顺序由字符串表示。字符 move[i] 表示其第 i 次移动。机器人的有效动作有 R（右），L（左），U（上）和
 * D（下）。如果机器人在完成所有动作后返回原点，则返回 true。否则，返回 false。
 * 
 * 注意：机器人“面朝”的方向无关紧要。 “R” 将始终使机器人向右移动一次，“L” 将始终向左移动等。此外，假设每次移动机器人的移动幅度相同。
 * 
 * 
 * 
 * 示例 1:
 * 
 * 输入: "UD"
 * 输出: true
 * 解释：机器人向上移动一次，然后向下移动一次。所有动作都具有相同的幅度，因此它最终回到它开始的原点。因此，我们返回 true。
 * 
 * 示例 2:
 * 
 * 输入: "LL"
 * 输出: false
 * 解释：机器人向左移动两次。它最终位于原点的左侧，距原点有两次 “移动” 的距离。我们返回 false，因为它在移动结束时没有返回原点。
 * 
 */
class Solution {
public:
    bool judgeCircle(string moves) {
        vector<int> res;
        res.push_back(0);
        res.push_back(0);
        for (int i = 0; i < moves.size(); i++)
        {
            switch (moves[i])
            {
            case 'U':
                res[1]++;
                break;
            case 'D':
                res[1]--;
                break;
            case 'L':
                res[0]--;
                break;
            case 'R':
                res[0]++;
                break;
            }
        }
        if (res[0] == 0 && res[1] == 0)
            return true;
        return false;
    }
};
//执行用时: 16 ms, 在Robot Return to Origin的C++提交中击败了93.49% 的用户
```

``` cpp
/*
 * @lc app=leetcode.cn id=661 lang=cpp
 *
 * [661] 图片平滑器
 *
 * https://leetcode-cn.com/problems/image-smoother/description/
 *
 * algorithms
 * Easy (44.71%)
 * Total Accepted:    1.9K
 * Total Submissions: 4.2K
 * Testcase Example:  '[[1,1,1],[1,0,1],[1,1,1]]'
 *
 * 包含整数的二维矩阵 M 表示一个图片的灰度。你需要设计一个平滑器来让每一个单元的灰度成为平均灰度 (向下舍入)
 * ，平均灰度的计算是周围的8个单元和它本身的值求平均，如果周围的单元格不足八个，则尽可能多的利用它们。
 * 
 * 示例 1:
 * 
 * 
 * 输入:
 * [[1,1,1],
 * ⁠[1,0,1],
 * ⁠[1,1,1]]
 * 输出:
 * [[0, 0, 0],
 * ⁠[0, 0, 0],
 * ⁠[0, 0, 0]]
 * 解释:
 * 对于点 (0,0), (0,2), (2,0), (2,2): 平均(3/4) = 平均(0.75) = 0
 * 对于点 (0,1), (1,0), (1,2), (2,1): 平均(5/6) = 平均(0.83333333) = 0
 * 对于点 (1,1): 平均(8/9) = 平均(0.88888889) = 0
 * 
 * 
 * 注意:
 * 
 * 
 * 给定矩阵中的整数范围为 [0, 255]。
 * 矩阵的长和宽的范围均为 [1, 150]。
 * 
 * 
 */
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& M) {
        vector<vector<int>> res; 
        for(int i = 0; i < M.size(); i++){
            vector<int> temp;
            for(int j = 0; j < M[i].size(); j++){
                int sum = 0;
                int count = 0;
                for(int m = i - 1; m <= i + 1; m++){
                    if(m<0||m>=M.size()) continue;
                    for(int n = j - 1; n <= j + 1; n++){
                        if(n<0||n>=M[m].size()) continue;
                        count++;
                        sum += M[m][n];
                    }
                }
                temp.push_back(sum/count);
            }
            res.push_back(temp);
        }
        return res;
    }
};
//执行用时: 128 ms, 在Image Smoother的C++提交中击败了97.66% 的用户
```

``` cpp
/*
 * @lc app=leetcode.cn id=559 lang=cpp
 *
 * [559] Maximum Depth of N-ary Tree
 *
 * https://leetcode-cn.com/problems/maximum-depth-of-n-ary-tree/description/
 *
 * algorithms
 * Easy (63.36%)
 * Total Accepted:    3.9K
 * Total Submissions: 6.1K
 * Testcase Example:  '{"$id":"1","children":[{"$id":"2","children":[{"$id":"5","children":[],"val":5},{"$id":"6","children":[],"val":6}],"val":3},{"$id":"3","children":[],"val":2},{"$id":"4","children":[],"val":4}],"val":1}'
 *
 * 给定一个 N 叉树，找到其最大深度。
 * 
 * 最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。
 * 
 * 例如，给定一个 3叉树 :
 * 
 * 
 * 
 * 
 * 
 * 
 * 
 * 我们应返回其最大深度，3。
 * 
 * 说明:
 * 
 * 
 * 树的深度不会超过 1000。
 * 树的节点总不会超过 5000。
 * 
 */
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    int maxDepth(Node* root) {
        if (!root)
            return 0;
        int res = 0;
        for (int i = 0; i < root->children.size(); i++)
        {
            res = max(res, maxDepth(root->children[i]));
        }
        return res + 1;
    }
};
//出现几次超时
```

