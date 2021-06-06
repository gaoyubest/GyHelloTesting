[TOC]

# HTTP请求码

此处添加HTTP状态码图
![](./)

## HTTP请求状态码为400

- 出现这个请求无效说明请求没有进入后台服务器里

- 原因：
  - （1）前端提交的字段名称或者字段类型和后台的实体类不一样 或者前端提交的参数跟后台需要的参数个数不一致，导致无法封装。
  - （2）前端提交到后台的数据应该是JSON字符串类型，而前端没有将对象转化为字符串类型；
解决方法：  对照字段名称，类型保证一致。

## HTTP请求状态码为404

- 请求URL存在空格或者换行符

## 状态码30X规范动作

301永久重定向

302临时重定向，HTTP1.0的状态码，HTTP1.1也有保留。 
如果client向server发送post请求。 
server返回URL和302。 
如果用户确认，client发送post请求。（但实际情况是，很多浏览器都不问问用户，直接变为get发送get请求）

303临时重定向，HTTP1.1的状态码// 
发送Post请求，收到303，直接重定向为get，发送get请求，不需要向用户确认

307临时重定向，HTTP1.1的状态码 
客户端发送post请求返回307时，浏览器询问用户是否再次post

## 对于307状态码说明
在 HTTP 协议中， 307 Temporary Redirect（临时重定向）是表示重定向的响应状态码，说明请求的资源暂时地被移动到 Location 首部所指向的 URL 上。

原始请求中的请求方法和消息主体会在重定向请求中被重用。在确实需要将重定向请求的方法转换为  GET 的场景下，可以考虑使用 303 See Also 状态码。例如在使用 PUT 方法进行文件上传操作时，需要返回确认信息（例如“你已经成功上传了xyz”）而不是上传的资源本身，就可以使用这个状态码。

状态码 307 与 302 之间的唯一区别在于，当发送重定向请求的时候，307 状态码可以确保请求方法和消息主体不会发生变化。当响应状态码为 302 的时候，一些旧有的用户代理会错误地将请求方法转换为 GET：使用非 GET 请求方法而返回 302 状态码，Web 应用的运行状况是不可预测的；而返回 307 状态码时则是可预测的。对于 GET 请求来说，两种情况没有区别。

[摘抄此链接，全部解释点击此链接](https://blog.csdn.net/idwtwt/article/details/90692773)