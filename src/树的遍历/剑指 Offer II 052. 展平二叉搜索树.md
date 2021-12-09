### 剑指 Offer II 052. 展平二叉搜索树

#### 题目地址

[剑指 Offer II 052. 展平二叉搜索树 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/NYBBNL/)

#### 解题思路

按照题目要求，直接中序遍历就可以了。我们需要做的是将中序遍历的结果存储下来，并转化为一颗新的树。其实也不难，按照模板走就好了

```java
LDR(root.left); // 中序遍历左子树
LDR(root); // 遍历根
LDR(root.right); // 中序遍历右子树
```

需要全局变量集合进行存储中序遍历的结果。然后对结果进行依次添加到右节点就好了。

#### 解题代码

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    private final LinkedList<Integer> values = new LinkedList<>();
    public TreeNode increasingBST(TreeNode root) {
        dfs(root);
        root.left = null;
        root.right = null;
        TreeNode pre = root;
        TreeNode node;
        for(Integer val : values){
            node = new TreeNode(val);
            pre.right = node;
            pre = pre.right;
        }
        return root.right;
    }
    private void dfs(TreeNode root){
        if(root.left != null)dfs(root.left);
        values.add(root.val);
        if(root.right != null)dfs(root.right);
    }
}
```

#### 提交记录

![提交记录](https://gitee.com/QingShanxl/pictures/raw/master/img//image-20211209235835582.png)