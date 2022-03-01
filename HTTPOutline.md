<!--  -->
# HTTP
HTTP（Hyper Text Transfer Protocol）直译超文本传输协议。

学习HTTP，要掌握基础概念、如何调试（如Node.js）、哪里查资料，以及标准文档（HTTP规格文档：RFC 2616等）。

## curl 命令
* 用 curl 可以发送HTTP请求。
  1. 如：curl -v <a>http://baidu.com</a>

<img src="images/i3.jpg" alt="Fig.3">

* 理解以下概念：
  1. url会被curl重写，先请求DNS获得IP。
  2. 进行TCP连接，TCP连接成功后，开始发送HTTP请求。
  3. 前缀为“>”的内容是请求内容。
  4. 前缀为“<”的内容是响应内容。
  5. 响应结束后关闭TCP连接。（代码中没有显示）
  6. 结束。

## HTTP请求与响应

<img src="images/i6.jpg" alt="Fig.6">

发送请求：可以使用curl命令简单地发送请求测试。协助用户发送请求的工具叫做“用户代理”(Uer Agent)。

做出响应：Node.js 有个http模块可以简单做到。

<img src="images/i7.jpg" alt="Fig.7">

* 以上举例了服务器响应代码。
* path 指不带查询参数地路径。
* response 是请求对象。
* 以上有两种字符串写法：1. `...`，这样写，在里边输入回车是会生效的。2. '...'，这样写，直接回车无效，需要用 \n 表示回车。
* response.write() 可以填写返回的内容。
* response.end() 表示响应可以发给用户了。
* <strong>注意：URL中的后缀是无效的，.../y.css 不一定是CSS内容。Content-Type=>类型/语法 才是决定文件类型的关键。</strong>

## HTTP 基础概念
### 请求
包括三部分（不算回车），可以参考 <a href="https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html">RFC 2616 第五章</a>：
1. 请求行：请求动词（GET/POST/PUT等）+路径和查询参数+协议名/版本
2. 请求头：
    
    Host: 域名或IP
    
    Accept: text/html
    
    Content-Type: 请求体的格式

3. 回车隔开
4. 请求体：请求体在GET请求中一般为空

### 响应
  
包括三部分（不算回车），<a href="https://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html">RFC 2616 第五章</a>：
1. 状态行：协议名/版本+状态码+状态字符串
2. Content-Type: 响应体的格式
3. 回车隔开
4. 响应体

常见状态码是前端<strong>考点</strong>。

### 构造请求和响应
* 用 curl 构造请求
  curl -v <a>http://127.0.0.1:8888</a>
  1. 设置请求动词：-X POST/GET（默认GET）
  2. 设置路径和查询参数：直接加在 url 后面
  3. 设置请求头：-H/--header 'Name: Value'
  4. 设置请求体：-d/--data '内容'

* 用 Node.js 读取请求
  1. 读取请求动词：request.method
  2. 读取路径：
      
      request.url 路径，带查询参数
      
      request.path 路径
      
      request.query 查询参数
  3. 读取请求头：request.headers['accept']
  4. 读取请求体

* 用 Node.js 设置响应
  1. 设置响应状态码：response.statusCode = XXX
  2. 设置响应头：response.setHeader('Content-Type','text/html')
  3. 设置响应体：response.write('内容')，这个方法可以多次调用，实现追加内容的效果。

* <strong>使用 console.log 来调试程序</strong>
  




