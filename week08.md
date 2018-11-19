# Algorithm

```Go
/*
Source  https://leetcode.com/problems/find-the-duplicate-number/
Author  Tian
Date    2018/11/17

287. Find the Duplicate Number

Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive),
prove that at least one duplicate number must exist. Assume that there is only one duplicate number,
find the duplicate one.

Example 1:

	Input: [1,3,4,2,2]
	Output: 2

Example 2:

	Input: [3,1,3,4,2]
	Output: 3

*/
package main

import (
	"fmt"
	"sort"
)

// solution 1
func findDuplicate(nums []int) int {
	sort.Ints(nums)
	for i := 1; i < len(nums); i++ {
		if nums[i] == nums[i-1] {
			return nums[i]
		}
	}
	return -1
}

// solution 2
func findDuplicate2(nums []int) int {
	tmp := make(map[int]bool)
	for _, value := range nums {
		if tmp[value] {
			return value
		}
		tmp[value] = true
	}
	return -1
}
```

# Review

reference https://medium.com/exploring-code/why-should-you-learn-go-f607681fad65

“Go will be the server language of the future.” — Tobias Lütke, Shopify

* Go has goroutines !!

Creating new thread in Java is not memory efficient. As every thread consumes approx 1MB of the memory heap size and eventually if you start spinning thousands of threads, they will put tremendous pressure on the heap and will cause shut down due to out of memory. Also, if you want to communicate between two or more threads, it’s very difficult.

Go has goroutines instead of threads. They consume almost 2KB memory from the heap. So, you can spin millions of goroutines at any time.

* Other benefits are :
   1. Goroutines have growable segmented stacks. That means they will use more memory only when needed.
   2. Goroutines have a faster startup time than threads.
   3. Goroutines come with built-in primitives to communicate safely between themselves (channels).
   4. Goroutines allow you to avoid having to resort to mutex locking when sharing data structures.  
   Also, goroutines and OS threads do not have 1:1 mapping. A single goroutine can run on multiple threads. Goroutines are multiplexed into small number of OS threads.

* Go runs directly on underlying hardware.

Go is compiled language. That means performance is almost nearer to lower level languages. It also uses garbage collection to allocation and removal of the object. So, no more malloc() and free() statements!!! Cool!!!

* Code written in Go is easy to maintain.

* Go is backed by Google.

# Technique

## Convert json to string
JSON.stringify({"name":"tian"})

## Java string convert to json

```Java
ObjectMapper om = new ObjectMapper();
try {
JsonNode node = om.readTree("{\"name\":\"value\"}");
JsonNode snode = node.get("name");
if (snode != null) {
  String name = snode.asText();
}

// add
((ObjectNode)node).put("name1", "value1");
```

## [Mysql DISTINCT](https://dev.mysql.com/doc/refman/8.0/en/distinct-optimization.html)

```sql
SELECT DISTINCT t.a FROM t;
```

## [Mysql EXPLAIN](https://dev.mysql.com/doc/refman/8.0/en/explain.html)

The DESCRIBE and EXPLAIN statements are synonyms. In practice, the DESCRIBE keyword is more often used to obtain information about table structure, whereas EXPLAIN is used to obtain a query execution plan (that is, an explanation of how MySQL would execute a query).

# Share

## Go Log

```Go
f, err := os.OpenFile(time.Now().Format("2006-01-02")+".log", os.O_RDWR | os.O_CREATE | os.O_APPEND, 0666)
if err != nil {
    log.Fatalf("error opening file: %v", err)
}
defer f.Close()

// just write file
log.SetOutput(f)

// write file and stdout
w := io.MultiWriter(os.Stdout, f)
log.SetOutput(w)

log.Println("This is a test log entry")
```
references
[SetOutput](https://golang.google.cn/pkg/log/#SetOutput)
[go-golang-write-log-to-file](https://stackoverflow.com/questions/19965795/go-golang-write-log-to-file)
