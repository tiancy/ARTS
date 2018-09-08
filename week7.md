# Algorithms

```Go
/*
Source  https://leetcode.com/problems/find-bottom-left-tree-value/description/
Author  Tian
Date    2018/09/08

513. Find Bottom Left Tree Value

Given a binary tree, find the leftmost value in the last row of the tree.

Example 1:
Input:

    2
   / \
  1   3

Output: 1

Example 2:
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output: 7

Related Topics
Tree, Depth-first Search, Breadth-first Search
*/
package main

// TreeNode Definition for a binary tree node.
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

var bl, v int

func findBottomLeftValue(root *TreeNode) int {
	bl, v = 0, 0
	dfs(root, 0)

	return v
}

func dfs(node *TreeNode, l int) {
	if node == nil {
		return
	}

	l++ // level
	dfs(node.Left, l)
	// record bottom left, and val
	if l > bl {
		bl = l
		v = node.Val
	}

	dfs(node.Right, l)
}

func main() {

}
```

# Review

## [Java String to InputStream](https://www.baeldung.com/convert-string-to-input-stream)

* Convert with Plain Java

```Java
String initialString = "text";
InputStream in = new ByteArrayInputStream(initialString.getBytes());
...
in.close();
}
```

* Convert with Guava

```Java
String initialString = "text";
InputStream in = new ReaderInputStream(CharSource.wrap(initialString).openStream());
...
in.close();
```

* Convert with Commons IO

```Java
String initialString = "text";
InputStream in = IOUtils.toInputStream(initialString);
...
in.close();
```

# Technique

## Go

```Go
// Monotonic Clocks
// reference https://golang.google.cn/pkg/time/#hdr-Monotonic_Clocks
start := time.Now()
... operation that takes 20 milliseconds ...
t := time.Now()
elapsed := t.Sub(start)

// time format
// reference https://stackoverflow.com/questions/20234104/how-to-format-current-time-using-a-yyyymmddhhmmss-format
time.Now().Format("2006-01-02 15:04:05")

// Convert reader to string
// reference https://stackoverflow.com/questions/9644139/from-io-reader-to-string-in-go
buf := new(bytes.Buffer)
buf.ReadFrom(Reader)
buf.String()

// Convert byte to string
//string(byte[:])
string(byte)

// Convert string to byte
[]byte(str)

// Convert string to int
strconv.Atoi(s)

// Convert interface to string
interfaceObj.(string) // if interfaceObj is nil, runtime error
fmt.Sprint(interfaceObj)

// mysql
// reference https://github.com/go-sql-driver/mysql/
import _ "github.com/go-sql-driver/mysql" //  go get -u github.com/go-sql-driver/mysql

sql.Open("mysql", "user:password@(address:port)/dbname")

// string to substring
str[strings.LastIndex(str, ","):]

// string replace
// Replace returns a copy of the string s with the first n non-overlapping instances of old replaced by new. If old is empty, it matches at the beginning of the string and after each UTF-8 sequence, yielding up to k+1 replacements for a k-rune string. If n < 0, there is no limit on the number of replacements.
strings.Replace(s, old, new, n)

// TrimSpace returns a slice of the string s, with all leading and trailing white space removed, as defined by Unicode.
strings.TrimSpace(" \t\n Hello, Gophers \n\t\r\n")
```

## Go read file lines from GBK encoding convert to UTF-8

```Go
import (
  sc "golang.org/x/text/encoding/simplifiedchinese"
  "golang.org/x/text/transform"
)

file, err := os.Open("filepath")
if err != nil {
  log.Fatal(err)
}
defer file.Close()

scanner := bufio.NewScanner(file)

for scanner.Scan() {
  text := bytes.NewBufferString(scanner.Text())
  ntext := transform.NewReader(text, sc.GBK.NewDecoder())
  str, err := ioutil.ReadAll(ntext)
  if err != nil {
    log.Fatal(err)
  }

  fmt.Printf("%s\n", string(str[:]))
}
```

References

[https://golang.org/pkg/bufio/#example_Scanner_lines](https://golang.org/pkg/bufio/#example_Scanner_lines)

[https://gist.github.com/zhangbaohe/c691e1da5bbdc7f41ca5](https://gist.github.com/zhangbaohe/c691e1da5bbdc7f41ca5)

## Go json marshal

```Go
// Escape HTML in data, "<br/>" --> "\u003cbr/\u003e"
json.Marshal(data)

// It is not escape HTML in data,  "<br/>" --> "<br/>"
var buf bytes.Buffer
e := json.NewEncoder(&buf)
e.SetEscapeHTML(false)
e.Encode(data)

fmt.Println(buf.String())
```

Reference [https://play.golang.org/p/OG-LA9XTmAm](https://play.golang.org/p/OG-LA9XTmAm)

## Go exec runs external commands for ffmpeg

```Go
cmd := exec.Command("/usr/local/bin/ffmpeg", "-i", inputUrl, "-ss", soundBegin, "-to", soundEnd, outputUrl)
cmd.run()
```

[ffmpeg](https://www.ffmpeg.org/ffmpeg.html#Automatic-stream-selection)

# Share

## 重复数据问题

前端发现数据出现重复问题，前一页和后一页， 怀疑后端接口有问题

解决问题思路
1. 查看数据有无重复数据
2. 怀疑分页插件有问题，是否用了无序列表
3. 根据排序字段查看数据，发现排序自段的数据一样，结果导致每次返回的数据顺序不一致
4. 增加排序字段ID，问题解决
