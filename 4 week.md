# Algorithm

```Go
/*
Source  https://leetcode.com/problems/same-tree/description/
Author  Tian
Created 2018/07/20

Given two binary trees, write a function to check if they are the same or not.
Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

Example 1:

Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]
        
Output: true
        
Example 2:

Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false

Related Topics 
Tree, Depth-first Search
*/
package main

// Definition for a binary tree node.
type TreeNode struct {
    Val int
    Left *TreeNode
    Right *TreeNode
}

var same bool
func isSameTree(p *TreeNode, q *TreeNode) bool {
    same = true
    dfs(p, q)
    return same
}

// Solution 1
// Depth first search
func dfs(p *TreeNode, q *TreeNode) {
    // if it was not same, return
    if !same || p == nil && q == nil {
        return
    }
    // one isn`t nil, one is nil, it is not same
    if p == nil || q == nil {
        same = false
        return
    }
    if p.Val != q.Val {
        same = false
        return
    }
    
    dfs(p.Left, q.Left)
    dfs(p.Right, q.Right)
}

func main() {

}
```

# Tip

## [RANKING IN MYSQL RESULTS](https://stackoverflow.com/questions/2520357/mysql-get-row-number-on-select)
```SQL
SELECT 
    rank
FROM
    (SELECT 
        @rank:=@rank + 1 AS rank, id
    FROM
        table_name t, (SELECT @rank:=0) r
    WHERE
         `order` >= (select `order` from table_name where id = 4) -- exclude id =4 after data
    ORDER BY `order` DESC) tmp
WHERE
    id = 4
```

## spring @RequestBody

```Java
@RequestMapping("/list")
public List<Object> list(@RequestBody Object obj) {
    // data...
    return null;
}
```
Headers Content-Type=application/json <br/>
Body {}, then request params is null, if it were otherwise, would be error HttpMessageNotReadableException: Required request body is missing

## set terminal color
export PS1="\[\e[30;1m\]\u@\h:\w\$\[\e[m\] "
alias ls='ls -G'
