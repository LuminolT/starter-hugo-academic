---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "A Simple Cors Issue"
subtitle: "后端开发手记，关于CORS接入封锁的解决"
summary: "后端开发手记，关于CORS接入封锁的解决"
authors: [admin]
tags: [Web Service, Back-end, Golang]
categories: []
date: 2021-09-19T10:12:01+08:00
lastmod: 2021-09-19T10:12:01+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## 跨域资源共享 CORS

### 技术性定义

跨域资源共享（Cross-Origin Resource Sharing）是一个系统，它由一系列传输的`HTTP`头组成，这些`HTTP`头决定浏览器是否阻止前端`JavaScript`代码获取跨域请求的响应。

### CORS Header

Access-Control-Allow-Origin
指示请求的资源能共享给哪些域。

Access-Control-Allow-Credentials
指示当请求的凭证标记为 true 时，是否响应该请求。

Access-Control-Allow-Headers
用在对预请求的响应中，指示实际的请求中可以使用哪些 HTTP 头。

Access-Control-Allow-Methods
指定对预请求的响应中，哪些 HTTP 方法允许访问请求的资源。

Access-Control-Expose-Headers
指示哪些 HTTP 头的名称能在响应中列出。

Access-Control-Max-Age
指示预请求的结果能被缓存多久。

Access-Control-Request-Headers
用于发起一个预请求，告知服务器正式请求会使用那些 HTTP 头。

Access-Control-Request-Method
用于发起一个预请求，告知服务器正式请求会使用哪一种 HTTP 请求方法。

Origin
指示获取资源的请求是从什么域发起的。

> 了解更多，推荐阅读：
> https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS

## 解决方法

### 响应头设置

让服务器设置一个响应头，允许浏览器向它发出跨域请求：

```
Access-Control-Allow-Origin: <Frontend_Server_IP>
```

当然更粗暴一点也可直接：

```
Access-Control-Allow-Origin: *
```

该方式表明 CORS 不考虑请求域，在开发时较为容易，但如果上线后会引起安全性问题（如构造POST请求）。

### Golang 代码实现

从网上找到了一个小小中间件：

```go
func CORSMiddleware() gin.HandlerFunc {
	return func(c *gin.Context) {
		c.Writer.Header().Set("Access-Control-Allow-Origin", "*")
		c.Writer.Header().Set("Access-Control-Allow-Credentials", "true")
		c.Writer.Header().Set("Access-Control-Allow-Headers", "Content-Type, Content-Length, Accept-Encoding, X-CSRF-Token, Authorization, accept, origin, Cache-Control, X-Requested-With")
		c.Writer.Header().Set("Access-Control-Allow-Methods", "POST, OPTIONS, GET, PUT")
		if c.Request.Method == "OPTIONS" {
			c.AbortWithStatus(204)
			return
		}
		c.Next()
	}
}
// Ref : https://stackoverflow.com/questions/29418478/go-gin-framework-cors
```

加入路由引擎中：

```go
r := gin.Default()
r.Use(CORSMiddleware())
```

就OK辽 o(*￣▽￣*)ブ