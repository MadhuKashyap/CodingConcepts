### Q. What is a binary tree?
Binary Tree is a non-linear data structure where each node has at most two children. Each node in a Binary Tree has three parts : data, 
left node, right node

### Q. What basic operations can be performed on binary tree?
* insert 
* delete
* search
* traverse (preorder, inorder, postorder)

### Q. Discuss the time complexities of above basic operations

Suppose we have a tree with N nodes
   #### CASE 1 : Binary Tree
   <span style="color:blue">some *This is Blue italic.* text</span>
   **search** : in a binary tree we will have to check all the elements, <span style="color:blue">So TC = average : O(N), worst : 0(N)</span> <br />
   **insert** : We first find the element whose leaf has to be inserted and then insert the leaf, So TC : average : O(N), worst : 0(N) <br />
   **delete** : we first find the element and then delete it, So TC : average : O(N), worst : 0(N) <br />


   #### CASE 2 : Binary Search Tree
   **search** : in a BST we will traverse only either left or right, So TC : O(log2N), worst( skewed tree) : 0(N) <br />
   **insert** : We first find the element traversing left or right then insert the leaf, So TC : O(log2N), worst( skewed tree) : 0(N) <br />
   **delete** : we first find the element and then delete it, So TC : O(log2N), worst( skewed tree) : 0(N) <br />                       
                                  
### Q. State some properties of binary tree

* If we create a binary tree using an array with N elements, height of the binary tree will be in range log2(N+1) <= height <= N.
* Number of nodes at level L of a binary tree is between [1 , 2^L].
* Total number of leaf nodes in a binary tree = (total number of nodes with 2 children) + 1

