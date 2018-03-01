---
layout:     post
title:      "PHP header函数用法"
subtitle:   "hearder 详解"
date:       2018-02-28 21:35:00
author:     "大业"
header-img: ""
catalog: true
tags:
    - PHP
    - 函数
---

* content
{:toc}

header() 函数相关用法说明





## 定义
header() 函数向客户端发送原始的 HTTP 报头

## 语法
header(string,replace,http_response_code)

|参数|描述|
|---|---|
|string|必选,规定要发送的报头字符串|
|replace|可选,指示该报头是否替换之前的报头,或添加第二个报头.默认是 true（替换）;false（允许相同类型的多个报头）|
|http_response_code|可选,把 HTTP 响应代码强制为指定的值|

## HTTP Request的Header信息
### 1. HTTP请求方式

|方 法|描 述|
|---|---|
|GET|向Web服务器请求一个文件|
|POST|向Web服务器发送数据让Web服务器进行处理|
|PUT|向Web服务器发送数据并存储在Web服务器内部|
|HEAD|检查一个对象是否存在|
|DELETE|从Web服务器上删除一个文件|
|CONNECT|对通道提供支持|
|TRACE|跟踪到服务器的路径|
|OPTIONS|查询Web服务器的性能|

**说明：**

主要使用到"GET"和"POST".

**实例：**

POST /test/tupian/cm HTTP/1.1
分成三部分：
1. POST：HTTP请求方式
2. /test/tupian/cm：请求Web服务器的目录地址（或者指令）
3. HTTP/1.1: URI（Uniform Resource Identifier，统一资源标识符）及其版本

*备注：*

    在Ajax中，对应method属性设置。


### 2. Host

**说明：**

请求的web服务器域名地址

**实例：**

例如:
```
web请求URL：http://www.baidu.com:8888/test/1

Host就为www.baidu.com:8888
```

## 常用设置
1. 页面没找到 Not Found
```php
header('HTTP/1.1 404 Not Found');
```

2. 用这个header指令来解决URL重写产生的404 header
```php
header('HTTP/1.1 200 OK');
```

3. 访问受限
```php
header('HTTP/1.1 403 Forbidden');
```
　　
4. 页面被永久删除，可以告诉搜索引擎更新它们的urls
```php
header('HTTP/1.1 301 Moved Permanently');
```

5. 服务器错误
```php
header('HTTP/1.1 500 Internal Server Error');
```

6. 重定向到一个新的位置
```php
header('Location: .example.org/');
```
　　
7. 延迟一段时间后重定向
```php
header('Refresh: 10; url=.example.org/');
```

8. 提示用户保存一个生成的 PDF 文件
```php
header("Content-type:application/pdf");
// 文件将被称为 downloaded.pdfheader("Content-Disposition:attachment;filename='downloaded.pdf'");
readfile("original.pdf");
// PDF 源在 original.pdf 中
```
　
9. 可以使用HTML语法来实现延迟
```php
header('Content-Transfer-Encoding: binary');
```

10. 禁止缓存当前文档
```php
header('Content-Transfer-Encoding: binary');
header（'Cache-Control: no-cache, no-store, max-age=0, must-revalidate'）;
header（'Expires: Mon, 26 Jul 2010 05:00:00 GMT'）;
header（'Pragma: no-cache'）;
```

11. 显示登录对话框,可以用来进行HTTP认证
```php
header（'HTTP/1.1 401 Unauthorized'）;
header（'WWW-Authenticate: Basic realm="Top Secret"'）;
```

12. 设置内容类型
```php
header（'Content-Type: text/html; charset=iso-8859-1'）;
header（'Content-Type: text/html; charset=utf-8'）;
header（'Content-Type: text/plain'）; // plain text file
header（'Content-Type: image/jpeg'）; // JPG picture
header（'Content-Type: application/zip'）; // ZIP file
header（'Content-Type: application/pdf'）; // PDF file
header（'Content-Type: audio/mpeg'）; // Audio MPEG （MP3,…） file
header（'Content-Type: application/x-shockwave-flash'）; // Flash animation
```
