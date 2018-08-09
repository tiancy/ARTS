# Algorithms

```Go
/*
Source  https://leetcode.com/problems/leaf-similar-trees/description/
Author  Tian
Date    2018/08/04
ID      872 Leaf-Similar Trees

Consider all the leaves of a binary tree.  From left to right order, the values of those leaves form a leaf value sequence.

For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).
Two binary trees are considered leaf-similar if their leaf value sequence is the same.
Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

Note:
Both of the given trees will have between 1 and 100 nodes.

Related Topics
Tree, Depth-first Search
*/

package main

// TreeNode Definition for a binary tree node.
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

func leafSimilar(root1 *TreeNode, root2 *TreeNode) bool {
	root1LN := make([]int, 0) // pull root1's lastNode
	root2LN := make([]int, 0) // pull root2's lastNode
	dfs(root1, &root1LN)
	dfs(root2, &root2LN)

	if len(root1LN) == len(root2LN) {
		// half on for
		for i, j := 0, len(root1LN)-1; i <= j; i, j = i+1, j-1 {
			// if had difference, return false
			if root1LN[i] != root2LN[i] || root1LN[j] != root2LN[j] {
				return false
			}
		}
		return true
	}
	return false
}

// Solution
// Depth first search
func dfs(node *TreeNode, lastNode *[]int) {
	if node == nil {
		return
	}
	// is lastNode
	if node.Left == nil && node.Right == nil {
		*lastNode = append(*lastNode, node.Val) // pull lastNode to slices
		return
	}
	dfs(node.Left, lastNode)
	dfs(node.Right, lastNode)
}

func main() {

}
```

# Review

[Escape to the Azores Islands, 1,000 Miles From Land]https://medium.com/s/greatescape/escape-to-the-azores-islands-1-000-miles-from-land-8b4740dc453c

Escape to the Azores Islands, I will

# Tip

## [Make the application executable](https://spring.io/guides/gs/rest-service-cors/#_make_the_application_executable)

@SpringBootApplication is a convenience annotation that adds all of the following:

* `@Configuration` tags the class as a source of bean definitions for the application context.
* `@EnableAutoConfiguration` tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
Normally you would add `@EnableWebMvc` for a Spring MVC app, but Spring Boot adds it automatically when it sees spring-webmvc on the classpath. This flags the application as a web application and activates key behaviors such as setting up a `DispatcherServlet`.
* `@ComponentScan` tells Spring to look for other components, configurations, and services in the same package, allowing it to find the controllers.

The main() method uses Spring Boot’s SpringApplication.run() method to launch an application. Did you notice that there wasn’t a single line of XML? No web.xml file either. This web application is 100% pure Java and you didn’t have to deal with configuring any plumbing or infrastructure.

## [VSCode Clean the workspace directory](https://github.com/redhat-developer/vscode-java/wiki/Troubleshooting#clean-the-workspace-directory)

In some occasions, deleting the Java Language Server workspace directory is helpful to go back to a clean slate.

MacOS : $HOME/Library/Application Support/Code[ - Variant]/User/workspaceStorage/

Build failed, do you want to continue?
Problem solved I resolved this issue by clearing the workspace cache in VS code.

## Mysql table data import

Table data export for insert on the Navicat,  then create temp same table,  execute insert,
data export for temp table to csv by your want, data import csv, configure import settings

## [Difference between decimal, float and double](https://stackoverflow.com/questions/618535/difference-between-decimal-float-and-double-in-net)

* float and double are floating binary point types.
* decimal is a floating decimal point type. 

As for what to use when:

* For values which are "naturally exact decimals" 
* For values which are more artefacts of nature which can't really be measured exactly anyway, float/double are more appropriate. 

# Share

## [Cross-Origin Resource Sharing (CORS)](https://spring.io/guides/gs/rest-service-cors/#_enabling_cors)
[blog post](https://spring.io/blog/2015/06/08/cors-support-in-spring-framework)<br/>
Cross-Origin Resource Sharing (CORS) is a technique for relaxing the same-origin policy, allowing Javascript on a web page to consume a REST API served from a different origin.

### Enabling CORS

* Controller method CORS configuration

@CrossOrigin(origins = "http://google.com")

* Global CORS configuration

```Java
@Configuration
public class MyConfiguration {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurerAdapter() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                  .allowedOrigins("http://example.com")
                  .allowedMethods("PUT", "DELETE")
                  .allowedHeaders("header1", "header2", "header3")
                  .exposedHeaders("header1", "header2")
                  .allowCredentials(false).maxAge(3600);
            }
        };
    }
}
```
