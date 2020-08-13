# Invert Binary Tree

Link : https://leetcode.com/problems/invert-binary-tree/

Invert a binary tree.

**Example:**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```



Basic Intuition

1. We observe that we have a few potential scenarios for nodes we might encounter

```
#1 : A node with one child

   	 4
   /   \
  None  2
  
#2 :  A node with two children
	   4
   /   \
  7     2
  
#3 : A Node with no children
	  4
   /   \
None     None

In Each case, we also observe that the end result is the same if we do a blanket swap of 

node.leftchild,node.rightchild = node.rightchild,node.leftchild
```

2. We observe that there are two cases that are trivially correct.
   1. A None Node (the child of a leaf node) has its children inverted by default
   2. A Leaf Node is inverted by default
3. Therefore we pick one of these as a base case and do a swap for everything else



### General Comments

1. Intuition was there but sometimes forgot to assign values to capture values from recursive functions

   ```
   Scenario 1
   x = 2
   recurseFunction(x)
   print(x)
   
   #x is 2
   
   
   Scenario 2
   x = 2
   recurseFunction(x)
   print(x)
   
   #x is not 2
   ```



### Python Solution

```python
class Solution:
    def invertTree(self, node: TreeNode) -> TreeNode:
        if not node:
            return None
        else:
            tmp = node.left
            node.left = self.invertTree(node.right)
            node.right = self.invertTree(tmp)
            return node
```





# Balanced Binary Tree

Link : https://leetcode.com/problems/balanced-binary-tree/

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of *every* node differ in height by no more than 1.

 

**Example 1:**

Given the following tree `[3,9,20,null,null,15,7]`:

```python
    3
   / \
  9  20
    /  \
   15   7
```

return True



### Basic Intuition

1. We should aim to do this recursively because height is recursively computed
2. It is trivially true that nodes or their leafs have a height of 1 and 0 respectively
3. Therefore we can build up the computation of the heights of individual subtrees through recursion



Python

```
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def helper(node):
            if not node.left and not node.right:
                return 1
            
            L = helper(node.left)
            if not L:
                return False
            
            R = helper(node.right)
            if not R:
                return False
            
            return abs(L-R)<=1 and max(L,R)+1
            
        if not root:
            return True
        
        return helper(root)
```



oCaml

```
type 'a tree = 
| Leaf 
| Node of 'a * 'a tree * 'a tree
    
    
let rec reverse tree = 
    match tree with
    | Leaf -> Leaf
    | Node (a,l,r) -> Node(a,reverse r,reverse l)
```

