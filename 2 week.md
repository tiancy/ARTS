# Algorithm

```Go
/*
Source  https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/description/
Author  tian
Created 2018/07/15

863. All Nodes Distance K in Binary Tree

We are given a binary tree (with root node root), a target node, and an integer value K.
Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.

Example 1:
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2
Output: [7,4,1]

Related Topics
Tree, Depth-first Search, Breadth-first Search
*/

package main

import (
	"fmt"
)

// TreeNode Definition for a binary tree node.
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

var parents map[TreeNode]TreeNode

func distanceK(root *TreeNode, target *TreeNode, K int) []int {
	if root == nil || target == nil {
		return nil
	}

	parents = make(map[TreeNode]TreeNode)
	dfs(root, &TreeNode{Val: -1})

	queue := make([]TreeNode, 0)
	queue = append(queue, TreeNode{Val: -1}) // push null
	queue = append(queue, *target)

	seen := make(map[TreeNode]TreeNode)
	seen[*target] = *target

	dist := 0
	for len(queue) != 0 {
		node := queue[0]  // Top (just get next element, don't remove it
		queue = queue[1:] // Discard top element
		if node.Val == -1 {
			if dist == K {
				ans := make([]int, 0)
				for _, v := range queue {
					ans = append(ans, v.Val)
				}
				return ans
			}
			queue = append(queue, TreeNode{Val: -1}) // push null, because add one depth after to ==
			dist++
		} else {
			// append node.Left, node.Right, node Parent to queue
			// if have one is distanceK when all is distanceK
			if node.Left != nil {
				// v != *node.Leftp, v is new object
				// if v, r := seen[*node.Left]; !r {
				// 	queue = append(queue, *node.Left)
				// 	seen[v] = v
				// }
				if _, r := seen[*node.Left]; !r {
					queue = append(queue, *node.Left)
					seen[*node.Left] = *node.Left
				}
			}
			if node.Right != nil {
				if _, r := seen[*node.Right]; !r {
					queue = append(queue, *node.Right)
					seen[*node.Right] = *node.Right
				}
			}
			p := parents[node]
			// node is't root
			if p.Val != -1 {
				if _, r := seen[p]; !r {
					queue = append(queue, p)
					seen[p] = p
				}
			}
		}
	}

	return nil
}

// dfs is depth first search
func dfs(node *TreeNode, parent *TreeNode) {
	if node != nil {
		parents[*node] = *parent
		dfs(node.Left, node)
		dfs(node.Right, node)
	}
}

func main() {
	n2 := &TreeNode{2, &TreeNode{7, nil, nil}, &TreeNode{4, nil, nil}}
	n5 := &TreeNode{5, &TreeNode{6, nil, nil}, n2}
	n0 := &TreeNode{0, nil, nil}
	root := TreeNode{3, n5, &TreeNode{1, n0, &TreeNode{8, nil, nil}}}
	r := distanceK(&root, n0, 4)
	fmt.Println(r)

	// n3 := &TreeNode{3, nil, nil}
	// root := TreeNode{0, &TreeNode{2, nil, nil}, &TreeNode{1, n3, nil}}
	// r := distanceK(&root, n3, 3)
	// fmt.Println(r)
}
```


# Review

[How I Fully Quit Google (And You Can, Too)](https://medium.com/s/story/how-i-fully-quit-google-and-you-can-too-4c2f3f85793a)

I like Google, but the world just that... 

We Reflection, We Change!


# Tip

## cmd native2ascii -reverse filepath 

[native2ascii](https://native2ascii.net) Convert national language characters to and from their Unicode equivalents in plain ASCII text.

## Required Storage and Range for Integer Types Supported by MySQL

Type | Storage (Bytes) | Minimum Value Signed |	Minimum Value Unsigned | Maximum Value Signed	| Maximum Value Unsigned
--- | --- | --- | --- | --- | ---
TINYINT | 1 | -128 | 0 | 127 | 255
SMALLINT |	2 |	-32768 | 0 | 32767 | 65535
MEDIUMINT |	3 |	-8388608 | 0 | 8388607 | 16777215
INT | 4 | -2147483648 | 0 | 2147483647 | 4294967295
BIGINT | 8 | -2^63 | 0 | 2^63-1 | 2^64-1

## [MyBatis Generator](http://www.mybatis.org/generator/index.html)

1.  [MyBatis GeneratorXML Configuration File Reference](http://www.mybatis.org/generator/configreference/xmlconfig.html)
2.  maven dependency
     ```
     <dependency>
         <groupId>org.mybatis.generator</groupId>
         <artifactId>mybatis-generator-core</artifactId>
         <version>1.3.5</version>
     </dependency>
     ```
3.  Run java
     ```java
     List<String> warnings = new ArrayList<String>();
     boolean overwrite = true;
     File configFile = new File("tmp/generatorConfig.xml");
     ConfigurationParser cp = new ConfigurationParser(warnings);
     Configuration config = cp.parseConfiguration(configFile);
     DefaultShellCallback callback = new DefaultShellCallback(overwrite);
     MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
     myBatisGenerator.generate(null);
     ```
     
## [@Resource vs @Autowired](https://stackoverflow.com/questions/4093504/resource-vs-autowired)

* @Resource allows you to specify a name of the injected bean
* @Resource means get me a known resource by name. The name is extracted from the name of the annotated setter or field, or it is taken from the name-Parameter.

* @Autowired allows you to mark it as non-mandatory.
* @Inject or @Autowired try to wire in a suitable other component by type.


# Share

## [utf8_unicode_ci vs utf8_general_ci by MySQL](https://forums.mysql.com/read.php?103,187048,188748#msg-188748)

### utf8_general_ci is a very simple collation. 

What it does - it just 
* removes all accents 
* then converts to upper case 
* uses the code of this sort of "base letter" result letter to compare. 

For example, these Latin letters: ÀÁÅåāă (and all other Latin letters "a" 
with any accents and in any cases) are all compared as equal to "A". 

### utf8_unicode_ci

* utf8_unicode_ci supports so called expansions and ligatures.
* utf8_unicode_ci is *generally* more accurate for all scripts. 

**The disadvantage of utf8_unicode_ci is that it is a little bit 
slower than utf8_general_ci.**

So when you need better sorting order - use utf8_unicode_ci, 
and when you utterly interested in performance - use utf8_general_ci.
