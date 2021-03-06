# Algorithm

```Go
/*
Source  https://leetcode.com/problems/maximum-depth-of-binary-tree/description/
Author  Tian
Created 2018/07/18

104. Maximum Depth of Binary Tree

Given a binary tree, find its maximum depth.
The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
Note: A leaf is a node with no children.

Related Topics 
Tree, Depth-first Search
*/
package main

import "fmt"

// Definition for a binary tree node.
type TreeNode struct {
    Val int
    Left *TreeNode
    Right *TreeNode
}

var depth int

func maxDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}
	depth = 0
	dfs(root, 0)
	// dfs2(root, 1)
	return depth
}

// solution 1
func dfs(node *TreeNode, level int) {
	if node == nil {
		if depth < level {
			depth = level
		}
		return
	}

	level++
	dfs(node.Left, level)
	dfs(node.Right, level)
}

// solution 2
func dfs2(node *TreeNode, level int) {
	if node.Left == nil && node.Right == nil {
		if depth < level {
			depth = level
		}
	} else {
		if node.Left != nil {
			dfs(node.Left, level + 1)
		}
		if node.Right != nil {
			dfs(node.Right, level + 1)
		}
	}
}

// solution 3, reference https://leetcode.com/problems/maximum-depth-of-binary-tree/discuss/34216/Simple-solution-using-Java
func maxDepth2(root *TreeNode) int {
	if root == nil {
		return 0
	}
    l := maxDepth(root.Left)
    r := maxDepth(root.Right)
    if l > r {
        return 1 + l
    }
    return 1 + r
}

func main() {
	n2 := &TreeNode{2, &TreeNode{7, nil, nil}, &TreeNode{4, nil, nil}}
	n5 := &TreeNode{5, &TreeNode{6, nil, nil}, n2}
	n0 := &TreeNode{Val:0}
	root := TreeNode{3, n5, &TreeNode{1, n0, &TreeNode{8, nil, nil}}}
	d := maxDepth(&root)
	fmt.Println(d)
}
```

# Review

## [5-Hour Rule](https://medium.com/the-mission/the-5-hour-rule-if-youre-not-spending-5-hours-per-week-learning-you-re-being-irresponsible-791c3f18f5e6?from=message&isappinstalled=0)

**“Intellectual capital will always trump financial capital.”** — Paul Tudor Jones, self-made billionaire entrepreneur, investor, and philanthropist

knowledge is the new money.But, unlike money, when you use knowledge or give it away, you don’t lose it. 

Working hard is the industrial era approach to getting ahead. **Learning hard is the knowledge economy equivalent.**

Don’t be lazy. Don’t make excuses. Just get it done.
“Live as if you were to die tomorrow. Learn as if you were to live forever.” — Mahatma Gandhi

# Tip

### [spring-boot hotswapping](https://docs.spring.io/spring-boot/docs/current/reference/html/howto-hotswapping.html)

Maven
```
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
		<optional>true</optional>
	</dependency>
</dependencies>
```

* Developer tools are automatically disabled when running a fully packaged application.
* Repackaged archives do not contain devtools by default.


### mybatis like
* select column from table where column like concat(#{selectContent}, '%'), 查询条件中使用函数会影响性能
* select column from table where column like '${selectContent}%', 可能会导致sql注入

### git commit

git config --global core.editor /usr/bin/vim

### vscode vim

Mac Setup

If key repeating isn't working for you, execute this in your Terminal, then restart VS Code.

```cmd
defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false         # For VS Code
defaults write com.microsoft.VSCodeInsiders ApplePressAndHoldEnabled -bool false # For VS Code Insider
defaults delete -g ApplePressAndHoldEnabled                                      # If necessary, reset global default
```

We also recommend going into System Preferences -> Keyboard and increasing the Key Repeat and Delay Until Repeat settings to improve your speed.


# Share

### [mybatis #{name} vs ${name}](http://www.mybatis.org/mybatis-3/sqlmap-xml.html#select)

* **#{id}**
This tells MyBatis to create a PreparedStatement parameter. With JDBC, such a parameter would be identified by a "?" in SQL passed to a new PreparedStatement, something like this:

```java
// Similar JDBC code, NOT MyBatis…
String selectPerson = "SELECT * FROM PERSON WHERE ID=?";
PreparedStatement ps = conn.prepareStatement(selectPerson);
ps.setInt(1,id);
```

* **${alias}**
This element can be used to define a reusable fragment of SQL code that can be included in other statements. It can be statically (during load phase) parametrized. Different property values can vary in include instances. For example:

```sql
<sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>
The SQL fragment can then be included in another statement, for example:

<select id="selectUsers" resultType="map">
  select
    <include refid="userColumns"><property name="alias" value="t1"/></include>,
    <include refid="userColumns"><property name="alias" value="t2"/></include>
  from some_table t1
    cross join some_table t2
</select>
```

* String Substitution

By default, using the #{} syntax will cause MyBatis to generate PreparedStatement properties and set the values safely against the PreparedStatement parameters (e.g. ?). While this is safer, faster and almost always preferred, sometimes you just want to directly inject an unmodified string into the SQL Statement. For example, for ORDER BY, you might use something like this:

ORDER BY ${columnName}
Here MyBatis won't modify or escape the string.

**NOTE** It's not safe to accept input from a user and supply it to a statement unmodified in this way. This leads to potential SQL Injection attacks and therefore you should either disallow user input in these fields, or always perform your own escapes and checks.

