# Algorithm

```Go
/*
Source  https://leetcode.com/problems/house-robber/description/
Author  tian
Date    2018/08/24

ID      198. House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example 1:

Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
			 Total amount you can rob = 1 + 3 = 4.

Example 2:

Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12

Related Topics
Dynamic Programming
*/

package main

// reference https://leetcode.com/problems/house-robber/discuss/55693/C-1ms-O(1)space-very-simple-solution
func rob(nums []int) int {
	if nums == nil || len(nums) == 0 {
		return 0
	}

	a, b := 0, 0
	for i, v := range nums {
		if i%2 == 0 {
			a = max(a+v, b) // a is add next a, so max(a+v, b), becuse current b is not adjacent next a
		} else {
			b = max(a, b+v)
		}
	}

	return max(a, b)
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

func main() {}

```

# Tip

## [safe update mode by mysql](https://stackoverflow.com/questions/11448068/mysql-error-code-1175-during-update-in-mysql-workbench)

Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.

Fixed Error

Try:

SET SQL_SAFE_UPDATES = 0;

Or you can modify your query to follow the rule (use primary key in where clause).

## Spring boot return html, annotated class is a "Controller", is not "RestController"

## Do not change property in the object getting, because insert data use getting, maybe it’s not you want

## vscode snippets

Preferences -> User snippets
```Json
// Example:
"Print to console": {
  "prefix": "log",
  "body": [
    "console.log('$1');",
    "$2"
  ],
  "description": "Log output to console"
}
```

# Review

## [OSS CopyFile](https://help.aliyun.com/document_detail/32149.html?spm=a2c4g.11186623.6.765.wZWvY4#拷贝文件)

```Go
import "github.com/aliyun/aliyun-oss-go-sdk/oss"

client, err := oss.New("Endpoint", "AccessKeyId", "AccessKeySecret")
if err != nil {
    // HandleError(err)
}

bucket, err := client.Bucket("my-bucket")
if err != nil {
    // HandleError(err)
}

// oss file path
_, err = bucket.CopyObject("my-object", "descObjectKey")
if err != nil {
    // HandleError(err)
}
```

## [OSS UploadFile](https://help.aliyun.com/document_detail/32147.html?spm=a2c4g.11186623.6.764.51sVYM#简单上传)

```Go
import "github.com/aliyun/aliyun-oss-go-sdk/oss"

client, err := oss.New("Endpoint", "AccessKeyId", "AccessKeySecret")
if err != nil {
    // HandleError(err)
}

bucket, err := client.Bucket("my-bucket")
if err != nil {
    // HandleError(err)
}

err = bucket.PutObjectFromFile("<yourObjectName>", "<yourLocalFile>")
if err != nil {
    fmt.Println("Error:", err)
    os.Exit(-1)
}
```
