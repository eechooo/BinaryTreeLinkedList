<h1>Binary Tree Linked List<h1>

<h2>897. Increasing Order Search Tree</h2>

这道题的重点是，先创建一个DummyNode节点, 设置一个current节点，在inorder traversal的时候,

current = DummyNode
current.right = root
root.left = null
current = prev

```
class Solution {
    TreeNode dummyNode = new TreeNode(-1);
    TreeNode prev = dummyNode;
    public TreeNode increasingBST(TreeNode root) {
        helper(root);
        return dummyNode.right;
    }
    public void helper(TreeNode root) {
        if (root == null) {
            return;
        }
        helper(root.left);
        prev.right = root;
        root.left = null;
        prev = root;
        helper(root.right);
    }
}
```

<h2>114. Flatten Binary Tree to Linked List</h2>

注意了这道题的解法是先遍历右边的节点，在遍历左边的节点，最后遍历根节点， for example

 		1
     2        3
   遍历右边的3，最后得到prev = 3, 这个时候，去遍历2， 2的左孩子，右孩子都为空，所以执行后面的 root.right = self.prev的操作，然后更新prev为当前的root, 返回上一层，上一层的root为
1，当然这一道题还有 iterative的做法

```
class Solution(object):
    def __init__(self):
        self.prev = None
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        if not root:
            return
        self.flatten(root.right)
        self.flatten(root.left)
        root.right = self.prev
        root.left = None
        self.prev = root
```

<h2>Flatten a Multilevel Doubly Linked List</h2>

这道题同样可以用DummyNode来做, 就是相当于树的遍历题，可以用bfs来做，因为child是需要放在前面的，所以stack里面应该先放node的next节点，再去放node的children节点, 

```
class Solution(object):
    def flatten(self, head):
        """
        :type head: Node
        :rtype: Node
        """
        if not head:
            return
        stack = [head]
        dummy = Node(0, None, head, None)
        prev = dummy
        
        while stack:
            root = stack.pop()
            
            root.prev = prev
            prev.next = root
            
            if root.next:
                stack.append(root.next)
                root.next = None
            if root.child:
                stack.append(root.child)
                root.child = None
            prev = root
        
        dummy.next.prev = None
        return dummy.next```





















