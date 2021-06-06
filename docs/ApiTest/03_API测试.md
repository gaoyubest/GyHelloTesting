[TOC]

# API测试

## 一、API测试工具介绍

[接口测试及工具详解](https://blog.csdn.net/weixin_39742065/article/details/110468142)

API（Application Programming Interface） 的测试往往是使用 API 测试工具，比如常见的命令行工具 cURL、图形界面工具 Postman 或者 SoapUI、API 性能测试的 JMeter等。


## 二、cURL安装及环境配置
[参考cURL配置及详细学习使用CSDN链接](https://blog.csdn.net/hadues/article/details/101788327)

[官方文档](https://www.gitbook.com/?utm_source=legacy&utm_medium=redirect&utm_campaign=close_legacy)

[Github主页](https://github.com/bagder/everything-curl)

[关于Curl 如何使用HTTP：官方文档](https://ec.haxx.se/http)

[cURL下载链接](https://curl.haxx.se/download.html)

windows下载：
![](./images/031_cURL下载.png)

- 新建系统变量：

```bash
CURL_HOME
F:\cURL\curl-7.73.0
```

![](./images/031_cURL环境变量配置1.png)

- 双击Path中添加这个环境变量:

```bash
%CURL_HOME%\bin\
```
![](./images/031_cURL环境变量配置2.png)

- 查看是否安装成功

```bash
curl --version
或
curl -v / --version

```

![](./images/031_cURL环境变量配置3.png)

- 查看参数

```bash
curl --help

C:\Users>curl --help
Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <CA certificate> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
     --cert-status   Verify the status of the server certificate
     --cert-type <type> Certificate file type (DER/PEM/ENG)
     --ciphers <list of ciphers> SSL ciphers to use
     --compressed    Request compressed response
```

## 三、cURL测试

### 1、通过以下命令发起 Account API 的调用

```bash
curl -i -H "Accept: application/json" -X GET "http://127.0.0.1:8080/account/ID008"

# 结果显示：
C:\Users\Gaoyu>curl -i -H "Accept: application/json" -X GET "http://127.0.0.1:8080/account/ID008"
HTTP/1.1 200
Content-Type: application/json;charset=UTF-8
Transfer-Encoding: chunked
Date: Fri, 04 Dec 2020 07:44:08 GMT

{"id":"ID008","type":"friends","email":"tom@api.io"}
```

```bash
这行命令中参数的含义如下：

第一个参数“-i”，说明需要显示 response 的 header 信息；
第二个参数“-H”，用于设定 request 中的 header；
第三个参数“-X”，用于指定执行的方法，这里使用了 GET 方法，其他常见的方法还有 POST、PUT 和 DELETE 等，如果不指定“-X”，那么默认的方法就是 GET。
最后“ http://127.0.0.1:8080/account/ID008 ”，指明了被测 API 的 endpoint 以及具体的 ID 值是“ID008”。
当使用 cURL 进行 API 测试时，常用参数还有两个：

“-d”：用于设定 http 参数，http 参数可以直接加在 URL 的 query string，也可以用“-d”带入参数。参数之间可以用“&”串接，或使用多个“-d”。
“-b”：当需要传递 cookie 时，用于指定 cookie 文件的路径。

需要注意的是这些参数都是大小写敏感的。
```

#### cURL参数设置

```bash
# 调试类
-v, --verbose                          输出信息
-q, --disable                          在第一个参数位置设置后 .curlrc 的设置直接失效，这个参数会影响到 -K, --config -A, --user-agent -e, --referer
-K, --config FILE                      指定配置文件
-L, --location                         跟踪重定向 (H)

# CLI显示设置
-s, --silent                           Silent模式。不输出任务内容
-S, --show-error                       显示错误. 在选项 -s 中，当 curl 出现错误时将显示
-f, --fail                             不显示 连接失败时HTTP错误信息
-i, --include                          显示 response的header (H/F)
-I, --head                             仅显示 响应文档头
-l, --list-only                        只列出FTP目录的名称 (F)
-#, --progress-bar                     以进度条 显示传输进度

# 数据传输类
-X, --request [GET|POST|PUT|DELETE|…]  使用指定的 http method 例如 -X POST
-H, --header <header>                  设定 request里的header 例如 -H "Content-Type: application/json"
-e, --referer                          设定 referer (H)
-d, --data <data>                      设定 http body 默认使用 content-type application/x-www-form-urlencoded (H)
    --data-raw <data>                  ASCII 编码 HTTP POST 数据 (H)
    --data-binary <data>               binary 编码 HTTP POST 数据 (H)
    --data-urlencode <data>            url 编码 HTTP POST 数据 (H)
-G, --get                              使用 HTTP GET 方法发送 -d 数据 (H)
-F, --form <name=string>               模拟 HTTP 表单数据提交 multipart POST (H)
    --form-string <name=string>        模拟 HTTP 表单数据提交 (H)
-u, --user <user:password>             使用帐户，密码 例如 admin:password
-b, --cookie <data>                    cookie 文件 (H)
-j, --junk-session-cookies             读取文件中但忽略会话cookie (H)
-A, --user-agent                       user-agent设置 (H)

# 传输设置
-C, --continue-at OFFSET               断点续转
-x, --proxy [PROTOCOL://]HOST[:PORT]   在指定的端口上使用代理
-U, --proxy-user USER[:PASSWORD]       代理用户名及密码

# 文件操作
-T, --upload-file <file>               上传文件
-a, --append                           添加要上传的文件 (F/SFTP)

# 输出设置
-o, --output <file>                    将输出写入文件，而非 stdout
-O, --remote-name                      将输出写入远程文件
-D, --dump-header <file>               将头信息写入指定的文件
-c, --cookie-jar <file>                操作结束后，要写入 Cookies 的文件位置
```

### 2、session场景

如果后端工程师使用 session 记录使用者登入信息，那么后端通常会传一个 session ID 给前端。之后，前端在发给后端的 requests 的 header 中就需要设置此 session ID，后端便会以此 session ID 识别出前端是属于具体哪个 session，此时 cURL 的命令行如下所示：

```bash
curl -i -H "sessionid:XXXXXXXXXX" -X GET "http://XXX/api/demoAPI"
```

### 3、cookie场景

成为文件，当需要再次使用该 cookie 时，再用“-b cookie_File” 的方式在 request 中植入 cookie 即可正常使用。具体的 cURL 的命令行如下所示：

```bash
# 将 cookie 保存为文件
curl -i -X POST -d username=robin -d password=password123 -c ~/cookie.txt "http://XXX/auth"
 
# 载入 cookie 到 request 中
curl -i -H "Accept:application/json" -X GET -b ~/cookie.txt "http://XXX/api/demoAPI"
```

cURL 只能发起 API 调用，而其本身并不具备结果验证能力（结果验证由人完成）

## 四、Postman测试

### 1、Postman下载及安装

[Postman下载链接](https://app.getpostman.com/app/download/win64)

[Postman学习链接](https://www.jianshu.com/p/97ba64888894)

- 下载完成后，双击即可安装
![](./images/032_Postman下载安装.png)

### 2、Postman使用

[Postman官方学习文档](https://learning.postman.com/docs/sending-requests/intro-to-collections/)

- Settings更改主题色为黑色

![](./images/032_Postman更改主题色.png)

- Postman界面介绍

![](./images/032_Postman使用1.png)

![](./images/032_Postman使用2.png)

### 3、Postman测试例子

#### （1）发起API调用

- endpoint 输入框中输入http://127.0.0.1:8080/account/ID_008
- 选择GET方法
- 点击Send按钮，发起API调用

![](./images/032_Postman使用3.png)
![](./images/032_Postman使用4.png)

- 返回的response默认以JSON文件的形式显示在Body中。

#### （2）添加结果验证

假定我们在 Account API 测试过程中有以下四个验证点：

- 请求的返回状态码（Status Code）应该是 200；
- 请求的响应时间应该小于 200 ms；
- 请求返回的 response header 中应该包含“Content-Type”参数；
- 请求返回的 response body 中，“type”的值应该是“friends”；

打开Test界面，点击SNIPPETS依次点击，自动生成代码：

- Status code: Code is 200
- Response time is less than 200 ms
- Response headers：Content-Type header check
- Response body: JSON value check
- 只修改代码13、15行即可

![](./images/032_Postman使用5.png)

测试通过：

![](./images/032_Postman使用6.png)

#### （3）保存测试用例

- Collection 来分类管理保存多个测试 request
- Save As 保存到Collection即可

#### （4）基于Postman的测试代码自动生成

![](./images/032_Postman使用7.png)

- 将Postman中的Collection导出为JSON文件

![](./images/032_Postman使用8.png)
![](./images/032_Postman使用9.png)

利用 Newman 工具直接执行 Postman 的 Collection

```bash
newman run examples/sample-collection.json;
```

### 五、安装newman

#### 1、安装nodejs

[点击此链接下载nodejs](http://nodejs.cn/download/)

- nodejs下载直接安装即可

```bash
# 查看是否安装成功
node -v

# 结果
C:\Users\Gaoyu>node -v
v14.15.1
```

#### 2、安装newman

```bash
npm install newman -global

C:\Users\Gaoyu>npm install newman -global
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
C:\Users\Gaoyu\AppData\Roaming\npm\newman -> C:\Users\Gaoyu\AppData\Roaming\npm\node_modules\newman\bin\newman.js
+ newman@5.2.1
added 157 packages from 199 contributors in 135.501s

# 查看是否安装成功
C:\Users\Gaoyu>newman -v
5.2.1

# 其他运行参数
C:\Users\Gaoyu>newman -h
Usage: newman [options] [command]

Options:
  -v, --version               output the version number
  -h, --help                  display help for command

Commands:
  run [options] <collection>  Initiate a Postman Collection run from a given URL or path

To get available options for a command:
  newman <command> -h

C:\Users\Gaoyu>newman --help
Usage: newman [options] [command]

Options:
  -v, --version               output the version number
  -h, --help                  display help for command

Commands:
  run [options] <collection>  Initiate a Postman Collection run from a given URL or path

To get available options for a command:
  newman <command> -h
```

#### 3、newman使用

- 找到Postman 的 Collection所在最小文件夹，按shift+右键，在此处打开Powershell
![](./images/033_newman使用1.png)

```bash
输入cmd 

PS G:\HelloMD\GyHelloTesting> cmd
Microsoft Windows [版本 10.0.18363.1198]
(c) 2019 Microsoft Corporation。保留所有权利。

newman run 加文件路径
# 文件路劲方法：输入 newman run api 后按Tab键自动补上当前文件夹中的api名字

G:\HelloMD\GyHelloTesting\TestDemo>newman run "API Test Demo.postman_collection.json"
newman: Newman v4 deprecates support for the v1 collection format
  Use the Postman Native app to export collections in the v2 format

newman

API Test Demo

→ AccountAPI
  GET http://127.0.0.1:8080/account/ID_008 [200 OK, 183B, 66ms]
  √  Status code is 200
  √  Response time is less than 200ms
  √  Content-Type is present
  √  My test asseret 001: type should be 'friends'

┌─────────────────────────┬──────────────────┬──────────────────┐
│                         │         executed │           failed │
├─────────────────────────┼──────────────────┼──────────────────┤
│              iterations │                1 │                0 │
├─────────────────────────┼──────────────────┼──────────────────┤
│                requests │                1 │                0 │
├─────────────────────────┼──────────────────┼──────────────────┤
│            test-scripts │                1 │                0 │
├─────────────────────────┼──────────────────┼──────────────────┤
│      prerequest-scripts │                0 │                0 │
├─────────────────────────┼──────────────────┼──────────────────┤
│              assertions │                4 │                0 │
├─────────────────────────┴──────────────────┴──────────────────┤
│ total run duration: 151ms                                     │
├───────────────────────────────────────────────────────────────┤
│ total data received: 53B (approx)                             │
├───────────────────────────────────────────────────────────────┤
│ average response time: 66ms [min: 66ms, max: 66ms, s.d.: 0µs] │
└───────────────────────────────────────────────────────────────┘
```

### 六、典型复杂场景

- 测试场景一：被测业务操作是由多个 API 调用协作完成
解决这个问题的核心思路是，通过网络监控的手段，捕获单个前端操作所触发的 API 调用序列。比如，通过类似于 Fiddler 之类的网络抓包工具，获取这个调用序列；又比如，目前很多互联网公司还在考虑基于用户行为日志，通过大数据手段来获取这个序列。


- 测试场景二：API 测试过程中的第三方依赖
解决这个问题的核心思路是，启用 Mock Server 来代替真实的 API

- 测试场景三：异步 API 的测试

> 异步 API 是指，调用后会立即返回，但是实际任务并没有真正完成，而是需要稍后去查询或者回调（Callback）的 API。

