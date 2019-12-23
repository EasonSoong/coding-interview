题目：输入两棵二叉树A和B，判断B是不是A的子结构。

题解：分为两部分，第一部分遍历二叉树A，寻找与B的根节点相同的值，找到之后到第二部分，遍历该结点与二叉树B，判断是否有相同的子节点。

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} s
 * @param {TreeNode} t
 * @return {boolean}
 */
var isSubtree = function(s, t) {
  let result = false;

  const _isSubtree = function(s1, t1) {
    if (!s1 && !t1) {
      return true;
    }
    if (!s1 || !t1) {
      return false;
    }
    if (s1.val === t1.val) {
      return _isSubtree(s1.left, t1.left) && _isSubtree(s1.right, t1.right);
    }
  }

  if (s && t) {
    if (s.val === t.val) {
      result = _isSubtree(s.left, t.left) && _isSubtree(s.right, t.right);
    }
    if (!result) {
      result = isSubtree(s.left, t);
    }
    if (!result) {
      result = isSubtree(s.right, t);
    }
  }

  return result;
};
```
