# Algorithm

[852. Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/description/)

Let's call an array A a mountain if the following properties hold:
	A.length >= 3
	There exists some 0 < i < A.length - 1 such that A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]

Given an array that is definitely a mountain, return any i such that A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1].

Example 1:
	Input: [0,1,0]
	Output: 1

Example 2:
	Input: [0,2,1,0]
	Output: 1

Note:

	3 <= A.length <= 10000

	0 <= A[i] <= 10^6

	A is a mountain, as defined above.

## Solution by Go
```Go
// binary search, find peak a mountain
func peakIndexInMountainArray(A []int) int {
	if len(A) < 3 || len(A) > 10000 {
		return -1
	}

	start := 0
	end := len(A) - 1

	for start+1 < end {
		mid := (start + end) / 2
		if A[mid] > A[mid-1] && A[mid] > A[mid+1] {
			return mid
		}
		if A[mid] > A[mid-1] {
			start = mid
		} else {
			end = mid
		}
	}
	return -1
}
```

# Review

[go defer](https://blog.learngoprogramming.com/golang-defer-simplified-77d3b2b817ff)

看了皓哥的专栏入了go的坑，不过已经喜欢上了go

这片文章主要讲如何使用defer语句，类似于finally

首先介绍了defer语句会在func结束前被执行

再介绍几个例子：

* 释放资源 Releasing acquired resources
![Releasing acquired resources](https://cdn-images-1.medium.com/max/2000/1*2gfaUL_WUKfwwR1m3Vynfg.png)

* Save us from panic
![Save us from panic](https://cdn-images-1.medium.com/max/2000/1*H0luK0YxgVlSkXqFsyhSnw.png)

* Deferred closure
![Deferred closure](https://cdn-images-1.medium.com/max/2000/1*kx5BnZbPHudssmhbXRNudw.png)

* Multiple defers
![Multiple defers](https://cdn-images-1.medium.com/max/2000/1*_s3_Lf92bz7W_U5EZPQSOA.png)



# Tip

* 本周学习的技术，来源工作，由于在做一个B端项目，要做前后端分离，之前没有做过
所以在网上查了一些资料，需要解决的问题是，用户状态，查到的解决方案为用JSON Web Token简称JWT
  1. 客户端向服务端发送登录请求
  2. 服务端验证，验证成功后生成一个Token，发送给客户端
  3. 客户端将Token保存，每次请求时要将Token发送给服务端
  4. 服务端接到请求，验证Token，验证成功向客户端返回请求的数据

    是否可以用cookie-session，这块还没有完全理解，下周继续学习

* 在工作中听同事讨论对于没有用到索引的问题, 可以强制使用索引的sql

    select id from table force index(PRI/index) 

# Share

[jwt](https://jwt.io/introduction/).
Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token.

* 疑问如果我拿到了Token是不是就可以登录了呢，那如何保证安全呢（好像可以xss攻击
* 信息都放到JWT中保存到客户端，是不是占有了更多的客户端空间

  思考，这块刚刚接触，还在考虑以何种方式做前后端分离，还得继续学习

    
