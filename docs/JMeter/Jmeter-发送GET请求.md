# Jmeter添加HTTP的GET请求

- 添加线程组
![](./../images/Jmeter-添加线程组.jpg)

- 发起HTTP请求
![](./../images/Jmeter-添加HTTP请求.jpg)

- HTTP请求参数
![](./../images/Jmeter-HTTP请求参数.jpg)

  - 注：默认为HTTP协议，可以不填
  - 参数（paramters）注意空格，域名的斜杠不能掉
  - 参数/消息体数据（bodydata）传参方式只能选一个。否则报错。消息体数据（bodydata）可传json、xml
  - ![](./../images/Jmeter-错误1.jpg)
  - ![](./../images/Jmeter-错误2.jpg)

- 添加代理
 ![](./../images/Jmeter-添加代理.jpg)
  
- 监听器->添加查看结果树
  ![](./../images/Jmeter-添加查看结果树.jpg)

- 添加HTTP的GET请求
[点此查看测试接口](https://www.juhe.cn/docs/api/id/65)
  ![](./../images/Jmeter-添加GET.jpg)

- 结果响应
  ![](./../images/Jmeter-GET响应.jpg)