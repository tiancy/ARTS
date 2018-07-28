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

# Review

## Why Being A Modern Polymath Is The New Normal

“Study the science of art. Study the art of science. Develop your senses — especially learn how to see. Realize that everything connects to everything else.” — Leonardo Da Vinci

Being a polymath instead of a specialist is an advantage, not a weakness.

If you want something extraordinary [in life], you have two paths:
1. Become the best at one specific thing.
2. Become very good (top 25%) at two or more things.

The first strategy is difficult to the point of near impossibility. Few people will ever play in the NBA or make a platinum album. I don’t recommend anyone even try.

The second strategy is fairly easy. Everyone has at least a few areas in which they could be in the top 25% with some effort. 

“In order to get into the top of the performance distribution, you have to escape from the crowd.” — Howard Marks, founder of Oaktree Capital 

“You can’t make money agreeing with the consensus view.” — Ray Dalio


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

## [srping @RestController](https://spring.io/guides/gs/rest-service-cors/#_create_a_resource_controller)

A key difference between a traditional MVC controller and the RESTful web service controller is the way that the HTTP response body is created. Rather than relying on a view technology to perform server-side rendering of the greeting data to HTML, this RESTful web service controller simply populates and returns a Greeting object. The object data will be written directly to the HTTP response as JSON.

To accomplish this, the @ResponseBody annotation on the greeting() method tells Spring MVC that it does not need to render the greeting object through a server-side view layer, but that instead the greeting object returned is the response body, and should be written out directly.

The Greeting object must be converted to JSON. Thanks to Spring’s HTTP message converter support, you don’t need to do this conversion manually. Because Jackson is on the classpath, Spring’s MappingJackson2HttpMessageConverter is automatically chosen to convert the Greeting instance to JSON.

## set terminal color

export PS1="\[\e[30;1m\]\u@\h:\w\$\[\e[m\] " <br/>
alias ls='ls -G'

# Share

## [Salt (cryptography)](https://en.wikipedia.org/wiki/Salt_(cryptography))

In cryptography, a salt is random data that is used as an additional input to a one-way function that "hashes" data, a password or passphrase.

* Example usage

Here is an incomplete example of a salt value for storing passwords. This first table has two username and password combinations. The password is not stored.

Username | Password
--- | ---
user1 | password123
user2 | password123

The salt value is generated at random and can be any length, in this case the salt value is 8 bytes (64-bit) long. The salt value is appended to the plaintext password and then the result is hashed, this is referred to as the hashed value. Both the salt value and hashed value are stored.

Username | Salt value | String to be hashed | Hashed value = SHA256 (Password + Salt value)
--- | --- | --- | ---
user1 | E1F53135E559C253 | password123+E1F53135E559C253 | 72AE25495A7981C40622D49F9A52E4F1565C90F048F59027BD9C8C8900D5C3D8
user2 | 84B03D034B409D4E | password123+84B03D034B409D4E | B4B6603ABC670967E99C7E7F1389E40CD16E78AD38EB1468EC2AA1E62B8BED3A

As the table above illustrates, different salt values will create completely different hashed values, even when the plaintext passwords are exactly the same. Additionally, dictionary attacks are mitigated to a degree as an attacker cannot practically precompute the hashes. However, a salt cannot protect against common or easily guessed passwords.

* Common mistakes(Don't do this)

1. Salt reuse
2. Short salt

* Benefits

1. Salts also combat the use of hash tables and rainbow tables for cracking passwords.
2. Another (lesser) benefit of a salt is as follows: two users might choose the same string as their password, or the same user might choose to use the same password on two machines. Without a salt, this password would be stored as the same hash string in the password file.
